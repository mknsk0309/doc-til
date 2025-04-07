# Bootstrapの導入

## DartSassのインストール

1. `Gemfile` に `dartsass-rails`, `foreman` を追加し、`bundle install` 実行する

   ```rb
   gem "dartsass-rails"
   .
   .
   .
   group :development do
     .
     .
     .
     gem "foreman", require: false
   end
   ```

2. `rails dartsass:install` で `RSpec` をインストールする

   - 実行後、以下のファイルが作成される
     - `app/assets/builds/.keep`
     - `app/assets/stylesheets/application.scss`
     - `Procfile.dev`
   - また、以下のファイルが変更される
     - `bin/dev`
     - `.gitignore`

3. `bin/dev` を実行し、動作確認を行う

   - 正常にインストールされていれば、以下の実行結果となる

     ```txt
     00:00:00 web.1  | Puma starting in single mode...
     00:00:00 web.1  | * Puma version: 6.6.0 ("Return to Forever")
     00:00:00 web.1  | * Ruby version: ruby 3.4.1 (2024-12-25 revision 48d4efcb85) +YJIT +PRISM [aarch64-linux]
     00:00:00 web.1  | *  Min threads: 3
     00:00:00 web.1  | *  Max threads: 3
     00:00:00 web.1  | *  Environment: development
     00:00:00 web.1  | *          PID: 56857
     00:00:00 web.1  | * Listening on http://127.0.0.1:3000
     00:00:00 web.1  | * Listening on http://[::1]:3000
     00:00:00 web.1  | Use Ctrl-C to stop
     00:00:00 css.1  | Sass is watching for changes. Press Ctrl-C to stop.
     00:00:00 css.1  | 
     ```

4. `app/assets/stylesheets/application.css` を削除する

   - `app/assets/stylesheets/application.scss` を使用するため、`.css` のファイルは不要

## Bootstrapのインストール

1. `Gemfile` に `bootstrap` を追加し、`bundle install` 実行する

   ```rb
   gem "bootstrap", "~> 5.3.0"
   ```

2. `app/assets/stylesheets/application.scss` に以下を追加する

   ```scss
   @import "bootstrap";
   ```

3. `config/importmap.rb` に以下を追加する

   ```rb
   pin "bootstrap", to: "bootstrap.min.js", preload: true
   pin "@popperjs/core", to: "popper.js", preload: true
   ```
