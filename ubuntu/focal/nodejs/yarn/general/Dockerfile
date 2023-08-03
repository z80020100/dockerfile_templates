FROM ubuntu:20.04
ENV WORKDIR="/app"
ENV HOME="/root"
WORKDIR $WORKDIR

# Set timezone
ENV CONTAINER_TIMEZONE="Asia/Taipei"
RUN ln -snf /usr/share/zoneinfo/$CONTAINER_TIMEZONE /etc/localtime && echo $CONTAINER_TIMEZONE > /etc/timezone

# Install required packages
RUN apt update && apt install -y autoconf build-essential curl gnupg locales tzdata wget && rm -rf /var/lib/apt/lists/*

# Set locale
RUN locale-gen en_US en_US.UTF-8
RUN update-locale LC_ALL=en_US.UTF-8 LANG=en_US.UTF-8
ENV LANG=en_US.UTF-8

# Install Node version management project 'n'
RUN cd /usr/local/bin \
    && wget https://raw.githubusercontent.com/tj/n/master/bin/n \
    && chmod +x /usr/local/bin/n

# Install Yarn
RUN curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add - \
    && echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list \
    && apt update \
    && apt install yarn -y

# Make sure n is available
RUN n -V

# Install Node.js via 'n'
RUN n lts

# Copy source code and installs all the dependencies defined in a package.json file
COPY . $WORKDIR/
RUN cd $WORKDIR && yarn install
