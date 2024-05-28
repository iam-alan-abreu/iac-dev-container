# You can pick any Debian/Ubuntu-based image. 😊
FROM mcr.microsoft.com/vscode/devcontainers/base:buster

# Defina a versão do Terragrunt
ENV TERRAGRUNT_VERSION=v0.58.10
ENV HADOLINGT_VERSION=v2.12.0

# INSTALL TERRAFORM
RUN wget -O- https://apt.releases.hashicorp.com/gpg | gpg --dearmor | tee /usr/share/keyrings/hashicorp-archive-keyring.gpg
RUN echo "deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com $(lsb_release -cs) main" | tee /etc/apt/sources.list.d/hashicorp.list

RUN apt update \
    && apt install -y --no-install-recommends \
    apt-utils \
    bash-completion \
    curl \
    git \
    gnupg \
    jq \
    lsb-release \
    lsof \
    openssh-client \
    python3 \
    python3-jmespath \
    python3-pip \
    python3-dev \
    build-essential \
    curl \
    libffi-dev \
    libssl-dev \
    tree \
    unzip \
    uuid-runtime \
    vim \
    zip \
    xz-utils \
    wget \
    unzip \
    terraform \
    direnv \
    && AZ_REPO=$(lsb_release -cs) \
    && echo "deb [arch=$(dpkg --print-architecture)] https://packages.microsoft.com/repos/azure-cli/ $AZ_REPO main" | tee /etc/apt/sources.list.d/azure-cli.list \
    && curl -sL https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor | tee /etc/apt/trusted.gpg.d/microsoft.gpg > /dev/null \
    && apt update \
    && apt install -y --no-install-recommends azure-cli="${AZ_VERSION}*" \
    && apt-get -y clean \
    && rm -fr /var/lib/apt/lists/* \
    && apt-get -y autoremove

# INSTALL PIP
RUN pip3 install --upgrade pip

# INSTALL CHECKOV
RUN pip3 install checkov

# INSTALL TERRAGRUNT
RUN curl -Lo /usr/local/bin/terragrunt https://github.com/gruntwork-io/terragrunt/releases/download/${TERRAGRUNT_VERSION}/terragrunt_linux_amd64 \
    && chmod +x /usr/local/bin/terragrunt

# INSTALL HADOLINT
RUN curl -L https://github.com/hadolint/hadolint/releases/download/${HADOLINGT_VERSION}/hadolint-Linux-x86_64 -o hadolint \
    && mv hadolint /usr/local/bin \
    && chmod +x /usr/local/bin/hadolint

# Set up direnv hook
RUN echo 'eval "$(direnv hook bash)"' >> ~/.bashrc
RUN echo 'eval "$(direnv hook bash)"' >> ~/.bash_profile