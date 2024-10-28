FROM cimg/go:1.23
ARG DOCKERIZE_VERSION="v0.6.1"

USER root
RUN apt-get update && \
    apt-get install -y \
        git-crypt \
        make \
        sshpass \
        awscli \
        tree \
        nodejs npm

RUN wget https://github.com/jwilder/dockerize/releases/download/$DOCKERIZE_VERSION/dockerize-linux-amd64-$DOCKERIZE_VERSION.tar.gz && \
    sudo tar -C /usr/local/bin -xzvf dockerize-linux-amd64-$DOCKERIZE_VERSION.tar.gz && \
    rm dockerize-linux-amd64-$DOCKERIZE_VERSION.tar.gz

USER circleci

RUN curl -o- -L https://slss.io/install | VERSION=3.27.0 bash

USER root

# somehow circle-ci does not pick up the PATH var from ~/.bashrc where the serverless-installer 
# added its bin-folder. so this is a quick-fix, for now
RUN ln -s /home/circleci/.serverless/bin/serverless /usr/local/bin/serverless

USER circleci
