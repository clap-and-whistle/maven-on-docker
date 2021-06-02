# 事前準備

```
mkdir ./backend/src
cd ./backend/src
git clone git@github.com:clap-and-whistle/spring-boot-demo.git
cd spring-boot-demo
git checkout dev
cd ../../..
cp ./.env.example ./.env
echo "OWNER_USER_ID=`id -u`" >> ./.env
```

# Dockerイメージのビルド実行

```
make init           # ビルド後、各コンテナが起動した状態になる
make log-mvn-watch  # mvnコンテナのログを標準出力へ垂れ流す
...

※Ctrl-C で抜ける
```

# spring-bootアプリケーションを起動する

```
make mvn                            # mvnコンテナへログイン
mvn spring-boot:run -Pdevelopment   # コンテナ内でmvnコマンドを実行
...

※ブラウザで http://localhost:3000 へアクセス
※Ctrl-C でアプリケーションを停止する
```

# Dockerコンテナ(mvn および db)の停止と再開

## 停止
```
make down
```

## 再開

```
make up
```