# 案件やリモート環境に応じてPHPバージョンは変える
# バージョンは docker-compose.yml の build.args 経由で .env の PHP_VERSION から渡される
ARG PHP_VERSION=8.5
FROM php:${PHP_VERSION}-apache

# ここで必要なものをインストール
RUN apt-get update \
 && apt-get install -y --no-install-recommends \
    gcc \
    make \
    git \
    zip \
    unzip \
    vim \
    libmcrypt-dev \
    curl \
    gnupg \
    libjpeg-dev \
    libfreetype6-dev \
    libjpeg62-turbo-dev \
    libpng-dev \
    libmcrypt-dev \
    libicu-dev \
    libonig-dev \
 && apt-get -y clean \
 && rm -rf /var/lib/apt/lists/* \
 && a2enmod rewrite headers


# 現在のphp公式イメージはOPcacheが静的に組み込まれている（php -m に Zend OPcache が出る）ので
# docker-php-ext-install の対象に opcache を入れるとビルドに失敗する
RUN docker-php-ext-install -j$(nproc) intl mysqli pdo_mysql && docker-php-ext-enable mysqli \
&& docker-php-ext-configure gd --with-freetype --with-jpeg \
&& docker-php-ext-install -j$(nproc) gd


   
COPY --from=composer:2 /usr/bin/composer /usr/bin/composer

# 予め docker cp コマンドで /usr/local/etc/php/php.ini-development ファイルをphp.iniとして持ってくる
# php.ini-production ではなく php.ini-development の方を持ってきた理由は、
# エラー出力関係が有効になっているから（例：display_errors = On）
COPY ./php.ini /usr/local/etc/php/php.ini

# /etc/apache2/sites-available/000-default.conf を予めホストにコピーしておいてDocumentRootを変更してコピーする
COPY ./000-default.conf /etc/apache2/sites-available/000-default.conf
