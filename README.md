# 事前準備

```
git clone git clone git@github.com:clap-and-whistle/spring-boot-demo.git
cd spring-boot-demo
git checkout dev
cd ..
cp ./backend/.env.example ./backend/.env
echo "OWNER_USER_ID=`id -u`" >> ./backend/.env
```

# Dockerイメージのビルド実行＆appコンテナへログイン

```
make init
make log-app-watch
...
Ctrl-C

make app
```
