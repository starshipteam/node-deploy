FROM cimg/go:1.18
ARG DOCKERIZE_VERSION="v0.6.1"

USER root
RUN apt-get update && \
    apt-get install -y git-crypt make sshpass awscli tree
RUN wget https://github.com/jwilder/dockerize/releases/download/$DOCKERIZE_VERSION/dockerize-linux-amd64-$DOCKERIZE_VERSION.tar.gz && \
    sudo tar -C /usr/local/bin -xzvf dockerize-linux-amd64-$DOCKERIZE_VERSION.tar.gz && \
    rm dockerize-linux-amd64-$DOCKERIZE_VERSION.tar.gz

USER circleci

RUN curl -o- -L https://slss.io/install | VERSION=2.66.1 bash
