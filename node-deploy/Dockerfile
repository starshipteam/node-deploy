FROM cimg/node:18.12.1
# Install required system packages and dependencies
USER root
# Do we still need IAM authentificator?
RUN mkdir -p /home/circleci/.local/bin/ && \
    wget -q -O /home/circleci/.local/bin/aws-iam-authenticator https://github.com/kubernetes-sigs/aws-iam-authenticator/releases/download/v0.4.0/aws-iam-authenticator_0.4.0_linux_amd64 && \
    chmod a+x /home/circleci/.local/bin/aws-iam-authenticator
RUN wget -q -O /home/circleci/.local/bin/kubectl https://dl.k8s.io/release/v1.25.7/bin/linux/amd64/kubectl && \
    chmod +x /home/circleci/.local/bin/kubectl
RUN wget -q -O /home/circleci/.local/bin/runIfChanged https://github.com/sgeisbacher/runIfChanged/releases/download/v0.10.1/runIfChanged.linux-amd64 && \
    chmod +x /home/circleci/.local/bin/runIfChanged
RUN apt-get update && \
    apt-get -y install \
      openssh-client \
      make \
      groff \
      git \
      silversearcher-ag \
      git-crypt
# Install aws CLI v2
RUN curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "/tmp/awscliv2.zip" && \
    unzip /tmp/awscliv2.zip -d /tmp && \
    /tmp/aws/install && \
    rm -rf /tmp/awscliv2.zip /tmp/aws
# Install Helm
RUN curl -fsSL https://raw.githubusercontent.com/helm/helm/master/scripts/get-helm-3 | bash
# Install kubeval binary
RUN mkdir -p /home/circleci/.local/bin/ && \
    curl -L https://github.com/instrumenta/kubeval/releases/latest/download/kubeval-linux-amd64.tar.gz | tar -C /home/circleci/.local/bin -xzf - kubeval && \
    chmod a+x /home/circleci/.local/bin/kubeval
RUN npm install -g zx yaml
# Install yq
RUN wget -qO /usr/local/bin/yq https://github.com/mikefarah/yq/releases/latest/download/yq_linux_amd64 &&\
    chmod a+x /usr/local/bin/yq
# Patching outdated kubeval Helm plugin in place
ENV HELM_KUBEVAL_VER=v0.16.1
RUN mkdir -p /home/circleci/.cache/helm/plugins/kubeval /home/circleci/.local/share/helm/plugins &&\
    git clone https://github.com/instrumenta/helm-kubeval /home/circleci/.cache/helm/plugins/kubeval &&\
    yq ".version = \"${HELM_KUBEVAL_VER}\"" -i /home/circleci/.cache/helm/plugins/kubeval/plugin.yaml &&\
    sed -i 's/v${version}/${version}/g' /home/circleci/.cache/helm/plugins/kubeval/scripts/install.sh
# Restore circleci user's home dir ownership
RUN chown -R circleci:circleci /home/circleci
USER circleci
# Install Helm pluging
RUN helm plugin install https://github.com/databus23/helm-diff &&\
    helm plugin install /home/circleci/.cache/helm/plugins/kubeval
RUN cd /home/circleci && npm link yaml

