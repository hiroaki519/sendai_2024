# Relicサマーインターン（26卒）のサンプルアプリだ!!
# 頑張ってvercelでデプロイします。
## 初回セットアップ手順（上から順番にコマンドを実行する）

```sh
# 作業ディレクトリに移動して作業を進めてください 

cp .env.example .env

#　以下はまとめてコピペして実行してください
docker run --rm \
    -u "$(id -u):$(id -g)" \
    -v "$(pwd):/var/www/html" \
    -w /var/www/html \
    laravelsail/php82-composer:latest \
    composer install

# 以下は一つずつ実行してください
docker-compose up -d
docker-compose exec laravel.test php artisan key:generate
docker-compose exec laravel.test php artisan migrate:fresh
docker-compose exec laravel.test npm install
docker-compose exec laravel.test npm run dev
```

ここまで実行すると http://localhost/ でサンプルアプリにアクセスできます

## 2回目以降の起動するときは下記のコマンドで実行する

```sh
docker-compose up -d
docker-compose exec laravel.test npm run dev
```

## 停止するときは下記のコマンドを実行する

```sh
docker-compose stop
```

## URLを押下して正常に動いているか確認する。
サンプルアプリ：http://localhost/

phpMyAdmin: http://localhost:8080/

## コマンドリファレンスは下記を参考にする。

```sh
# MySQLコンソールにログイン
docker-compose exec mysql mysql -u sail -p'password' example_app

# キャッシュ削除
docker-compose exec laravel.test php artisan cache:clear
docker-compose exec laravel.test php artisan config:clear
docker-compose exec laravel.test php artisan route:clear
docker-compose exec laravel.test php artisan view:clear
docker-compose exec laravel.test php artisan clear-compiled

# Laravel実行コンテナにログイン
docker-compose exec laravel.test /bin/bash
```
