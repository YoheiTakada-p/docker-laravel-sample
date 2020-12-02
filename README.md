# docker-laravel-sample

http://127.0.0.1:10080  

下記を参考に作成  
https://qiita.com/ucan-lab/items/56c9dc3cf2e6762672f4  

イメージを作成する  
$ docker-compose build  
コンテナを作成する  
$ docker-compose up -d  
Laravelをインストールする(git.ignoreのため)  
$ docker-compose exec app bash  
composer.lockからインストール  
$ composer install  
envファイルがないのでenv.exampleをコピー  
[app] $ cp .env.example .env  
.envにAPP_KEYの値がないので、生成  
参考 → https://qiita.com/yk2220s/items/dcbf54c6d1f33a0cb06f  
[app] $ php artisan key:generate
.envのSQLの情報を修正する  
  .env  
    DB_CONNECTION=mysql    
    DB_HOST=db  
    DB_PORT=3306  
    DB_DATABASE=laravel_local  
    DB_USERNAME=phper  
    DB_PASSWORD=secret  
マイグレーションする  
参考 → https://note.com/kodokuna_dancer/n/n68c8ef4c7af3
$ php artisan migrate

MySQL接続　
$ docker-compose exec db bash -c 'mysql -u${MYSQL_USER} -p${MYSQL_PASSWORD} ${MYSQL_DATABASE}'  
  or  
[app] mysql -u $MYSQL_USER -p$MYSQL_PASSWORD $MYSQL_DATABASE  

Laravelのログをコンテナログに表示する   
backend/.envを修正する  
  .env  
    LOG_CHANNEL=stderr  

backend/routes/web.phpを書き換える    
  web.php  
    Route::get('/', function () {  
        logger('welcome route.');  
        return view('welcome');  
});  
$ docker-compose logs  
-f でログウォッチ  
$ docker-compose logs -f  
サービス名を指定してログを表示  
$ docker-compose logs -f app  
対話シェル  
[app] $ php artisan tinker  
