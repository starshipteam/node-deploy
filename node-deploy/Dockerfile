FROM cimg/node:16.1.0
# Install required system packages and dependencies
USER root
RUN mkdir -p /home/circleci/.local/bin/ && \
    wget -q -O /home/circleci/.local/bin/aws-iam-authenticator https://github.com/kubernetes-sigs/aws-iam-authenticator/releases/download/v0.4.0/aws-iam-authenticator_0.4.0_linux_amd64 && \
    chmod a+x /home/circleci/.local/bin/aws-iam-authenticator
RUN wget -q -O /home/circleci/.local/bin/kubectl https://storage.googleapis.com/kubernetes-release/release/v1.16.0/bin/linux/amd64/kubectl && \
    chmod +x /home/circleci/.local/bin/kubectl
RUN wget -q -O /home/circleci/.local/bin/runIfChanged https://github.com/sgeisbacher/runIfChanged/releases/download/v0.10.1/runIfChanged.linux-amd64 && \
    chmod +x /home/circleci/.local/bin/runIfChanged
RUN apt-get update && \
    apt-get -y install openssh-client make
RUN apt-get -y install python3-pip &&\
    apt-get -y install groff &&\
    pip3 install awscli
RUN apt-get -y install git-crypt
RUN curl -fsSL https://raw.githubusercontent.com/helm/helm/master/scripts/get-helm-3 | bash
RUN mkdir -p /home/circleci/.local/bin/ && \
    curl -L https://github.com/instrumenta/kubeval/releases/latest/download/kubeval-linux-amd64.tar.gz | tar -C /home/circleci/.local/bin -xzf - kubeval && \
    chmod a+x /home/circleci/.local/bin/kubeval  
RUN npm install -g zx
USER circleci
