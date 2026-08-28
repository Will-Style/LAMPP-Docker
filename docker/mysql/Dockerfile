# 使うMySQLのバージョンは docker-compose.yml の build.args 経由で .env の MYSQL_VERSION から渡される
# 9.x 系からは Debian ベースのイメージが廃止され Oracle Linux ベースのみになっている
ARG MYSQL_VERSION=9.7
FROM mysql:${MYSQL_VERSION}

# MySQLが載ってるOSの日本語ロケールを有効にする
# Oracle Linux ベースなので apt-get ではなく microdnf を使う
RUN microdnf install -y glibc-langpack-ja \
 && microdnf clean all

ENV LANG=ja_JP.UTF-8
ENV LANGUAGE=ja_JP:ja
ENV LC_ALL=ja_JP.UTF-8

# MySQL設定ファイルをイメージ内にコピー（/etc/my.cnf から !includedir されている）
COPY ./my.cnf /etc/mysql/conf.d/my.cnf

#docker runに実行される
CMD ["mysqld"]
