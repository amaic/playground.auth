FROM mcr.microsoft.com/dotnet/sdk:10.0

RUN apt-get update
RUN apt-get install -y --no-install-recommends \
    git \
    curl \
    wget \
    unzip \
    apt-transport-https \
    ca-certificates \
    software-properties-common \
    bash-completion \
    iputils-ping \
    net-tools \
    nano \
    sudo \
    jq \
    yq 

RUN bash <<-"EOD"
    source /etc/os-release && \
    wget -q https://packages.microsoft.com/config/ubuntu/$VERSION_ID/packages-microsoft-prod.deb && \
    dpkg -i packages-microsoft-prod.deb && \
    rm packages-microsoft-prod.deb && \
    apt-get update && \
    apt-get install -y powershell
EOD

RUN dotnet completions script bash > /etc/bash_completion.d/dotnet-completions.bash

RUN userdel --remove ubuntu
ARG DOCKER_GID
RUN groupadd --gid ${DOCKER_GID} docker
RUN useradd --create-home --uid 1000 --shell /bin/bash --groups sudo,docker vscode
RUN echo "vscode ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers

USER vscode
WORKDIR /home/vscode
ENV force_color_prompt=true

