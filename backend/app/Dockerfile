FROM maven:3-openjdk-11
LABEL maintainer="clap-and-whistle <kimita@clap-and-whistle.page>"
SHELL ["/bin/bash", "-oeux", "pipefail", "-c"]

ARG OWNER_USER_ID
ARG OWNER_GROUP_ID

RUN curl -sL https://deb.nodesource.com/setup_14.x | bash - && \
  apt-get update && \
  apt-get install -y nodejs && \
  npm install -g gulp-cli && \
  groupadd -g $OWNER_USER_ID webapp && \
  useradd -u $OWNER_USER_ID -g $OWNER_GROUP_ID webapp && \
  mkdir /home/webapp && \
  chown webapp:webapp /home/webapp

WORKDIR /work/maven

EXPOSE 8080

ENTRYPOINT [ "/bin/bash", "-c" ]
CMD [ "jshell" ]
