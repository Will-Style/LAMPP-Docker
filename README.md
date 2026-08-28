#### .envの[example]の箇所をすべて案件名に変更してください

```
# Compose のプロジェクト名: [example]の箇所を変更
COMPOSE_PROJECT_NAME=example
# コンテナ間通信用のネットワーク名: [example]の箇所を変更
APP_NETWORK=example-network

# ホスト名: [example]の箇所を変更
VIRTUAL_HOST=example.local.localhost
# phpmyadminのホスト名: [example]の箇所を変更
MYADMIN_HOST_NAME=example-db.local.localhost
```

`APP_NETWORK` は案件ごとに必ずユニークな名前にしてください。
ここが他の案件と重複していると、同じネットワーク上に `mysql` という名前のコンテナが
複数並ぶことになり、アプリやphpMyAdminが別案件のDBに繋がってしまいます。
（結果として案件を1つずつしか起動できなくなります）


#### 下記コマンドを実行してください。

```
$ docker compose up -d --build
```
###### ホストに接続
https://[example].local.localhost でアクセス可能になります。

###### PHPMyAdminに接続
https://[example]-db.local.localhost



###### 注意点
- PHPは8.5、MySQLは9.7(LTS)を使用しています。バージョンは .env の `PHP_VERSION` と `MYSQL_VERSION` で切り替えられます。
- MySQLは9.x系からDebianベースのイメージが廃止されOracle Linuxベースになっています。`MYSQL_VERSION` を 8.0 以前に下げる場合は `./docker/mysql/Dockerfile` のパッケージ導入部分を `apt-get` に書き換えてください。
- phpMyAdminは .env の `MYSQL_ROOT_USER` / `MYSQL_ROOT_PASSWORD` で自動ログインします。ログイン画面でユーザーを選びたい場合は docker-compose.yml の `PMA_USER` と `PMA_PASSWORD` をコメントアウトしてください。
- Apacheのログは .env の `APACHE_LOG_DIR`（既定は ./log/web/）に出力されます。
- ./docker/mysql/init/内にsqlファイルを入れて初回起動するとsqlを実行してくれます。
- ./docker/mysql/db/内でデータを永続化しているのでやり直したいときはフォルダ内を削除してから再度起動してください。

```
$ docker compose down --volumes
$ docker compose up -d --build
```

###### Apache-PHPのホストに接続する方法
```
$ docker compose exec web bash
```
###### MySQLのホストに接続する方法
```
$ docker compose exec mysql bash
```
