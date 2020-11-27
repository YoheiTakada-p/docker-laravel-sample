#ベースイメージ
FROM mysql:8.0
#mysqlの環境変数 DATABASEはイメージ起動時に作成されるデータベース名
#デフォルトでrootユーザーが作成される(スーパーユーザー)
#USER,PASSWORD　ユーザー作成とパスワード生成　スーパーユーザーではないけど権限はある
#ROOT_PASSWORDはスーパーユーザーだよ　rootに対するパスワード生成
ENV MYSQL_DATABASE=laravel_local \
  MYSQL_USER=phper \
  MYSQL_PASSWORD=secret \
  MYSQL_ROOT_PASSWORD=secret \
  TZ=Asia/Tokyo

COPY ./my.cnf /etc/mysql/conf.d/my.cnf

RUN chmod 644 /etc/mysql/conf.d/my.cnf
