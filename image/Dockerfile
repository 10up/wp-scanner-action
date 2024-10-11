FROM debian:stable-slim

ARG PHP_VERSION=8.2

LABEL "com.github.actions.name"="WordPress Scanner Action"
LABEL "com.github.actions.description"="Scan WordPress sites for plugins and themes vulnerabilities, PHP syntax and viruses"
LABEL "com.github.actions.icon"="shield"
LABEL "com.github.actions.color"="blue"

LABEL maintainer="10upbot <10upbot+github@10up.com>"
LABEL version="v1.0.1"
LABEL repository="https://github.com/10up/wp-scanner-action"

RUN apt-get update \
	&& apt-get install -y curl \
    apt-transport-https \
    ca-certificates \
    clamav \
    clamav-freshclam \
    git \
    jq \
    lsb-release \
    mariadb-server \
    rsync \
    subversion \
    unzip \
    wget \
	&& apt-get clean -y \
	&& rm -rf /var/lib/apt/lists/* 

# Install PHP
RUN wget -O /etc/apt/trusted.gpg.d/php.gpg https://packages.sury.org/php/apt.gpg \
  && echo "deb https://packages.sury.org/php/ $(lsb_release -sc) main" | tee /etc/apt/sources.list.d/php.list \
  && apt update \
  && apt install -y \
  php${PHP_VERSION} \
  php${PHP_VERSION}-bcmath \
  php${PHP_VERSION}-bz2 \
  php${PHP_VERSION}-cli \
  php${PHP_VERSION}-curl \
  php${PHP_VERSION}-gd \
  php${PHP_VERSION}-imagick \
  php${PHP_VERSION}-intl \
  php${PHP_VERSION}-mbstring \
  php${PHP_VERSION}-memcache \
  php${PHP_VERSION}-memcached \
  php${PHP_VERSION}-mysql \
  php${PHP_VERSION}-opcache \
  php${PHP_VERSION}-redis \
  php${PHP_VERSION}-soap \
  php${PHP_VERSION}-xml \
  php${PHP_VERSION}-xmlrpc \
  php${PHP_VERSION}-zip \
  && apt-get clean -y \
  && rm -rf /var/lib/apt/lists/*

# Install WPCLI
RUN curl -o /usr/local/bin/wp https://raw.githubusercontent.com/wp-cli/builds/gh-pages/phar/wp-cli.phar && \
    chmod +x /usr/local/bin/wp

# Install Composer
RUN curl -o /usr/local/bin/composer https://getcomposer.org/composer-2.phar && \
    chmod +x /usr/local/bin/composer

## Update clamav definitions ##
RUN /usr/bin/freshclam

COPY entrypoint.sh /entrypoint.sh
RUN chmod +x /entrypoint.sh
ENTRYPOINT ["/entrypoint.sh"]