FROM php:fpm

# 各パッケージのダウンロードにはZIP拡張を使用するので入れておく
RUN apt-get update \ 
    && apt-get install -y zlib1g-dev \
    && docker-php-ext-install zip

# composerインストール
RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" \
  && php -r "if (hash_file('SHA384', 'composer-setup.php') === '544e09ee996cdf60ece3804abc52599c22b1f40f4323403c44d44fdfdd586475ca9813a858088ffbc1f233e9b180f061') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;" \
  && php composer-setup.php \
  && php -r "unlink('composer-setup.php');" \
  && mv composer.phar /usr/local/bin/composer

# 質問を受けずにrootで`composer install`する
# https://getcomposer.org/doc/03-cli.md#composer-allow-superuser
# If set to 1, this env disables the warning about running commands as root/super user. It also disables automatic clearing of sudo sessions, so you should really only set this if you use Composer as super user at all times like in docker containers.
ENV COMPOSER_ALLOW_SUPERUSER 1
# グローバルパッケージのインストール先変更
ENV COMPOSER_HOME /composer
# composerのパスを通す
ENV PATH $PATH:/composer/vendor/bin

#Larabel
RUN composer global require "laravel/installer"

#プロジェクトを作成
# RUN laravel new sample

# プロジェクト名はnginxのルートと揃えてやる
# root /src/sample/public;

# PHP's DB setting
RUN apt-get update \
    && apt-get install -y libpq-dev \
    && docker-php-ext-install pdo_mysql pdo_pgsql

# Install Node.js
RUN apt-get update \
    && apt-get install -y gnupg2 \
    && curl -sL https://deb.nodesource.com/setup_8.x | bash - \
    && apt-get install -y nodejs

WORKDIR /src