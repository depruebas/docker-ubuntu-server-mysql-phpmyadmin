# Use Ubuntu 24.04 as base image
FROM ubuntu:24.04

# Avoid interactive prompts during package installation
ENV DEBIAN_FRONTEND=noninteractive

ENV TZ=Europe/Madrid
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

# Update and install basic packages and Apache2, MySql, PHP and mods apache2
RUN apt-get update && apt-get install -y \
    apache2 php mysql-server \
    php-mysqli php-mbstring php-zip php-gd php-json php-curl libapache2-mod-php \
    curl \
    wget \
    tar \
    nano \
    vim \
    net-tools \
    iputils-ping \
    systemd \
    sudo \
    iproute2 iputils-ping locales \
    && apt-get clean && rm -rf /var/lib/apt/lists/*

# Set spanish language
RUN locale-gen es_ES.UTF-8
RUN echo 'echo "LANG=es_ES" > /etc/default/locale'
ENV LC_ALL=es_ES.UTF-8

RUN echo '%sudo ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers

# Create directories 
RUN mkdir -p /opt/start && mkdir /data

COPY ./provision/entrypoint.sh /opt/start/entrypoint.sh
RUN chmod +x /opt/start/entrypoint.sh 

# Configure apache2
COPY ./provision/apache-vhost.conf /opt/start/apache-vhost.conf
RUN ln -s /opt/start/apache-vhost.conf  /etc/apache2/sites-enabled/apache-vhost.conf
RUN rm /etc/apache2/sites-enabled/000-default.conf
RUN sed -i '$aListen 8080' /etc/apache2/ports.conf
RUN echo "ServerName localhost" >> /etc/apache2/apache2.conf

WORKDIR /home/ubuntu

# Default command (optional)
ENTRYPOINT ["/opt/start/entrypoint.sh"]
