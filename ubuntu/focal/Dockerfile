# https://code.visualstudio.com/remote/advancedcontainers/add-nonroot-user
FROM ubuntu:20.04

ARG USERNAME=docker
ARG USER_UID=1000
ARG USER_GID=$USER_UID
ENV HOME="/home/$USERNAME"

# Set timezone
ENV CONTAINER_TIMEZONE="Asia/Tokyo"
RUN ln -snf /usr/share/zoneinfo/$CONTAINER_TIMEZONE /etc/localtime && echo $CONTAINER_TIMEZONE >/etc/timezone

# Install required packages
RUN apt update && apt install -y autoconf bash-completion build-essential curl git gnupg locales sudo tzdata wget && rm -rf /var/lib/apt/lists/*
# https://docs.docker.com/develop/develop-images/dockerfile_best-practices/
# Official Debian and Ubuntu images automatically run apt-get clean, so explicit invocation is not required.

# Set locale
RUN locale-gen en_US en_US.UTF-8
RUN update-locale LC_ALL=en_US.UTF-8 LANG=en_US.UTF-8
ENV LANG=en_US.UTF-8

# Create the user
RUN groupadd --gid $USER_GID $USERNAME && useradd --uid $USER_UID --gid $USER_GID -m $USERNAME

# Add sudo support
RUN echo $USERNAME ALL=\(root\) NOPASSWD:ALL >/etc/sudoers.d/$USERNAME && chmod 0440 /etc/sudoers.d/$USERNAME

WORKDIR $HOME
USER $USERNAME
