# summary
mysqlをすぐに使えるようにしたdocker-composeである。
以下、3つのサービスが起動する。
mysql_server: mysqlサーバー
mysql_client: mysqlクライアント
adminer: mysql GUIクライアント

・ホストの3306ポートがmysqlサーバーにバインドされている。
・ホストの8080ポートがadminerにバインドされている。
・パスワード等の環境変数は.envファイルを編集する事で反映される。
・initディレクトリに配置されたスクリプトで、初期データベースの構築がされる。

# operation
docker-compose up -d

docker-compose down

## mysql_server
docker exec -it mysql_server bash

mysql -u root -ppass -h localhost

use library;

select * from booktable;

## mysql_client
docker exec -it mysql_client sh

mysql -u root -ppass -h mysql_server

## adminer
http://localhost:8080
host: mysql_server
user: root
pass: pass
db: library

# tips
## 文字化け
クライアントから接続した時に、日本語が文字化けすることがある。
my.cnfの権限が不適切で、誰でも書き込みが出来る場合にファイルが読み込まれない事が原因なので権限を変更する。
windowsの場合はファイルを右クリック→プロパティ→属性を読み取り専用とする。

