# Herokuへのデプロイ手順

## 1. Herokuの操作のためにheroku-cliというコマンドラインツールを導入する。

$ wget https://cli-assets.heroku.com/heroku-linux-x64.tar.gz -O heroku.tar.gz

$ sudo mkdir -p /usr/local/lib/heroku

$ sudo tar --strip-components 1 -zxvf heroku.tar.gz -C /usr/local/lib/heroku

$ sudo ln -s /usr/local/lib/heroku/bin/heroku /usr/local/bin/heroku
<br />

## 2. Herokuへログイン

$ heroku login -i

heroku: Enter your login credentials
Email: Herokuに登録済みのメールアドレスを入力
Password: Herokuに登録済みのパスワードを入力
Logged in as 上記メールアドレスがココに表示されます

## 3. Herokuアプリの新規作成

$ heroku create 任意のアプリ名（大文字・_(アンダーバー)はNG）


