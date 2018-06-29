# Laravel 環境構築

## 環境構築時のバージョン

* PHP 7.2.6
* Laravel Framework 5.6.26
* node v8.11.3
* npm 5.6.0
* mysql Ver 14.14 Distrib 5.7.22
* nginx 1.15.0

## ファイル

```
/
|   docker-compose.yml
|   README.md
|
+---nginx
|       default.conf
|
+---php
|       Dockerfile
|
\---src
        index.html
        info.php
```

## Usage

### Laravelプロジェクト作成

プロジェクト名"project"を作成する。  
このディレクトリで作業する。

1. `docker-compose build`
2. `docker-compose up -d`
3. `docker-compose exec php laravel new project`  
project は*src*ディレクトリに作成される  

#### project名の変更

`docker-compose exec php laravel new project` コマンド実行時の**project**を任意の名前に変更。

*nginx/default.conf*に記載される`root /src/project/public;`のprojectを任意の名前に変更。

`docker-compose down & docker-compose up -d`で再ビルド。

### ブラウザ確認

1. `docker-machine ls`でURLを確認し、8080ポートで確認する

## 補足

mysql8.0 ではデフォルトの認証形式を mysql_native_password から caching_sha2_password に変更
されていて、PHPのmysql 認証はmysql_native_passwordがデフォルトになっているため、
caching_sha2_password に変更する必要がある。

この環境ではcaching_sha2_password に変更はいしないようにするため
mysqlのバージョンは5系最新を使用している。

-------------------------------------

## 参考

[Dockerでいい感じにPHP(Laravel)のローカル開発環境を作る](https://qiita.com/IganinTea/items/aec8f2b15b203946a2c4)
