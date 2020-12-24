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

Creating ⬢ アプリ名... done
https://アプリ名-[任意の名前].herokuapp.com/ 
https://git.heroku.com/アプリ名.git

アプリ名と同時に、Gitにリモートリポジトリとして「heroku」のリポジトリが作られる

heroku apps
アプリ名がきちんと登録されたか確認

$ git remote -v
heroku  https://git.heroku.com/アプリ名.git(fetch)
heroku  https://git.heroku.com/アプリ名.git(push)
origin  https://github.com/ユーザー名/アプリ名.git  (fetch)
origin  https://github.com/ユーザー名/アプリ名.git (push)

1. 設定ファイルの作成

$ echo "web: vendor/bin/heroku-php-apache2 public/" > Procfile

※必ずlaravel-questのプロジェクト直下で実行

サーバソフトはapache2を指定

プロジェクト直下に Procfile ファイルが生成される
git add .

git commit -m "add procfile"
[main *******] add procfile
 2 files changed, 1 insertion(+)
 create mode 100*** Procfile
 create mode 100*** heroku.tar.gz

2. デプロイ

git push heroku main ←ブランチ名 要確認!

完了するとURLが表示される
remote:        https://アプリ名.herokuapp.com/ deployed to Heroku

表示確認　この時にデータベースを作ってないならエラーが出る

Whoops, looks like something went wrong

以下のコマンドで参考にデバッグモードを使用すると
heroku config:add APP_DEBUG=true
Whoops, looks like something went wrong.

(2/2) QueryException
SQLSTATE[HY000] [2002] Connection refused (SQL: select count(*) as aggregate from `users`)

データベースの問題が表示される

あと、参考にURLを取得したいときのコマンドは

$ heroku apps:info

3. 環境変数の確認  $ heroku config:set APP_KEY=$(php artisan --no-ansi key:generate --show)

$ heroku config

=== アプリ名 Config Vars
APP_KEY: 設定されたAPP_KEYが表示される

上記二つのコマンドでAPP_KEYの一致を確認する。あとは.envも
