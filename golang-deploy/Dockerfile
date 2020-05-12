FROM circleci/golang:1.13
USER root
RUN apt-get update && \
    apt-get install -y npm git-crypt make sshpass awscli
RUN npm install -g serverless
USER circleci
