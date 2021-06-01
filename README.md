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

# Dockerイメージのビルド実行＆appコンテナへログイン

```
make init
make log-app-watch
...
Ctrl-C

make app
```
