FROM maven:3-openjdk-11
LABEL maintainer="clap-and-whistle <kimita@clap-and-whistle.page>"
SHELL ["/bin/bash", "-oeux", "pipefail", "-c"]

RUN curl -sL https://deb.nodesource.com/setup_14.x | bash - && \
  apt-get update && \
  apt-get install -y nodejs && \
  npm install -g gulp-cli

WORKDIR /work/maven

EXPOSE 8080

ENTRYPOINT [ "/bin/bash", "-c" ]
CMD [ "jshell" ]
