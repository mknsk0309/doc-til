# RSpecの導入

## RSpecのインストール

1. `Gemfile` に `rspec-rails` を追加し、`bundle install` 実行する

   ```rb
   group :development, :test do
      gem "rspec-rails", require: false
   end
   ```

   - `require: false` はアプリ起動時、自動読み込みされないようにするためのオプション
   - 起動時のメモリ消費を抑え、アプリケーションの起動速度を向上させることができる

2. `rails g rspec:install` で `RSpec` をインストールする

   - 実行後、以下のファイルが作成される
     - `.rspec`
     - `spec/spec_helper.rb`
     - `spec/rails_helper.rb`

3. `bundle exec rspec` を実行し、動作確認を行う

   - 正常にインストールされていれば、以下の実行結果となる

     ```txt
     No examples found.


     Finished in 0.00016 seconds (files took 0.06845 seconds to load)
     0 examples, 0 failures
     ```

## FactoryBotのインストール

- テストデータを作成するためのライブラリ

1. `Gemfile` に `factory_bot_rails` を追加し、`bundle install` 実行する

   ```rb
   group :development, :test do
      gem "rspec-rails", require: false
      gem "factory_bot_rails"
   end
   ```

## Faker のインストール

- ダミーデータを作成するためのライブラリ

1. `Gemfile` に `factory_bot_rails` を追加し、`bundle install` 実行する

   ```rb
   group :development, :test do
      gem "rspec-rails", require: false
      gem "factory_bot_rails"
      gem "faker", require: false
   end
   ```

## 環境設定

1. `config/application.rb` に RSpec の設定を追加する

   ```rb
   # config.generators.system_tests = nil がある場合は削除しておく
   module SampleApp
     class Application < Rails::Application
       .
       .
       .
       config.generators do |g|
         g.test_framework :rspec,
           fixtures: true,        # テストデータを作成する
           view_specs: false,     # ビュースペックを作成しない
           helper_specs: false,   # ヘルパースペックを作成しない
           request_specs: false,  # リクエストスペックを作成しない
           routing_specs: false   # ルーティングスペックを作成しない
         # テストデータの出力先を指定する
         g.fixture_replacement :factory_bot, dir: "spec/factories"
       end
     end
   end
   ```

2. `spec/rails_helper.rb` に FactoryBot の設定を追加する

   - 以下により、FactoryBot クラスの呼び出しを簡略化できる

   ```rb
   RSpec.configure do |config|
     .
     .
     .
     config.include FactoryBot::Syntax::Methods
   end
   ```

3. `.rspec` を以下のように変更する

   ```config
   --require spec_helper
   --color
   --format documentation
   ```

   - `--format documentation`
     - テスト結果を読みやすい形式で表示する
     - テストの進行状況や失敗したテストの詳細を把握しやすくなる

   - `--color`
     - テスト結果を色分けして表示する
     - 成功、失敗、保留などの結果を視覚的に区別しやすくなる

## GitHub Actions の設定

以下のジョブを追加する。

```yml
name: CI

on:
  pull_request:
  push:
    branches: [ main ]

jobs:
  .
  .
  .
  rspec:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout code
        uses: actions/checkout@v4

      - name: Set up Ruby
        uses: ruby/setup-ruby@v1
        with:
          ruby-version: .ruby-version
          bundler-cache: true

      - name: Run RSpec tests
        run: bundle exec rspec
  .
  .
  .
```
