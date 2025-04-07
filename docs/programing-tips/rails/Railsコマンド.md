# Rails コマンド

## アプリケーションの作成

```bash
rails new
```

オプション等は [こちら](https://railsguides.jp/command_line.html#rails-new) を参照。

## サーバの起動

```bash
rails server
rails s
```

- オプション
  - `-p` : リッスンするポートを指定
  - `-e` : サーバの環境を指定 (デフォルトは `development`)
  - `-b` : バインドする IP アドレスを指定
  - `-d` : サーバをデーモンとして起動

- 実行例：
  
  ```bash
  rails s -e production -p 4000
  ```

## テンプレートを用いた生成

```bash
rails generate ...
rails g ...
```
