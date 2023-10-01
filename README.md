#### .envのVIRTUAL_HOSTとMYADMIN_HOST_NAMEのexampleを変更してください

```
# ホスト名: [example]の箇所を変更
VIRTUAL_HOST=example.local.localhost
# phpmyadminのホスト名: [example]の箇所を変更
MYADMIN_HOST_NAME=example-db.local.localhost
```


#### 下記コマンドを実行してください。

```
$ docker-compose up -d --build
```
###### ホストに接続
https://[example].local.localhost でアクセス可能になります。

###### PHPMyAdminに接続
https://[example]-db.local.localhost



###### 注意点
- PHPのVersionは7.4でMySQLは5.7にしてますが各Dockerfile内で変更できるようにしています。
- laravel-dockerとなっていますがDocumentRootを変更すればWordPressも動くと思います。
- ./docker/mysql/init/内にsqlファイルを入れて初回起動するとsqlを実行してくれます。
- ./docker/mysql/db/内でデータを永続化しているのでやり直したいときはフォルダ内を削除してから再度起動してください。

```
$ docker compose down --volumes
$ docker compose up -d --build
```

###### Apache-PHPのホストに接続する方法
```
$ docker-compose exec web bash
```
###### MySQLのホストに接続する方法
```
$ docker-compose exec mysql bash
```