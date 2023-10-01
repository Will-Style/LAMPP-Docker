#使うDockerイメージはdocker-compose.ymlで指定
FROM mysql:5.7

# MySQLが載ってるOSのタイムゾーンを日本時間にする
# 参考URL<https://qiita.com/rowpure/items/dbedbe2b98e91a34d0d5>
# 他にベストの方法があれば模索してもいい
RUN apt-get update
RUN apt-get install -y tzdata && \
    cp /usr/share/zoneinfo/Asia/Tokyo /etc/localtime

#MySQL設定ファイルをイメージ内にコピー
ADD ./my.cnf /etc/mysql/conf.d/my.cnf

#docker runに実行される
CMD ["mysqld"]