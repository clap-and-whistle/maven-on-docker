###############################################################################
# Dockerイメージをビルドする時点で、SpringBootアプリケーションが依存ライブラリの取得を済ませておく
###############################################################################
FROM maven:3-openjdk-11 AS builder
LABEL maintainer="clap-and-whistle <kimita@clap-and-whistle.page>"
SHELL ["/bin/bash", "-oeux", "pipefail", "-c"]

ARG HOST_BACKEND_SRC_PATH

ADD ./$HOST_BACKEND_SRC_PATH /tmp/work
WORKDIR /tmp/work

RUN mvn install -Dmaven.test.skip


###############################################################################
# 非rootユーザで動作するDockerコンテナで mvn spring-boot:run を実行できるようにする
###############################################################################
FROM maven:3-openjdk-11 AS runner
LABEL maintainer="clap-and-whistle <kimita@clap-and-whistle.page>"
SHELL ["/bin/bash", "-oeux", "pipefail", "-c"]

# ホスト側のユーザIDとシェルログイン時のユーザIDを一致させる (target/配下の生成物等がrootの所有とならないように)
ARG OWNER_USER_ID
ARG OWNER_GROUP_ID

RUN curl -sL https://deb.nodesource.com/setup_14.x | bash - && \
  apt-get update && \
  apt-get install -y nodejs && \
  groupadd -g $OWNER_USER_ID webapp && \
  useradd -u $OWNER_USER_ID -g $OWNER_GROUP_ID webapp && \
  mkdir -p /home/webapp/.m2 && \
  chown -R webapp:webapp /home/webapp

WORKDIR /work/maven

# builderステージのコンテナで取得した依存ライブラリを runnerコンテナへコピーすることでcacheの振る舞いをさせる
COPY --from=builder --chown=webapp:webapp /root/.m2 /home/webapp/.m2/

EXPOSE 8080

ENTRYPOINT [ "/bin/bash", "-c" ]
CMD [ "jshell" ]

