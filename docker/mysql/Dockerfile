#使うDockerイメージはdocker-compose.ymlで指定
FROM mysql:8.0-debian

# MySQLが載ってるOSのタイムゾーンを日本時間にする
# 参考URL<https://qiita.com/rowpure/items/dbedbe2b98e91a34d0d5>
# 他にベストの方法があれば模索してもいい
# RUN echo "deb http://archive.debian.org/debian/ stretch main" > /etc/apt/sources.list \
#     && echo "deb http://archive.debian.org/debian-security stretch/updates main" >> /etc/apt/sources.list \
#     && apt-get update \
#     && apt-get install -y tzdata && \
#     cp /usr/share/zoneinfo/Asia/Tokyo /etc/localtime

RUN apt-get update
RUN apt-get -y install locales-all

ENV LANG ja_JP.UTF-8
ENV LANGUAGE ja_JP:ja
ENV LC_ALL ja_JP.UTF-8

#MySQL設定ファイルをイメージ内にコピー
ADD ./my.cnf /etc/mysql/conf.d/my.cnf

#docker runに実行される
CMD ["mysqld"]