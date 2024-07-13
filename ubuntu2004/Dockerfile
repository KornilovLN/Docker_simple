#---------------------------------------------------------------------------------------------
# Образ базового контейнера для создания остальных докер-сервисов 
#
# Команда создания базового образа:  
# docker build -t base_image .
#
# Команда запуска для интерактивного режима
# docker run -it --rm -v ~/virt/dockers/ubuntu2004/shared_folder:/app/shared_folder base_image
#---------------------------------------------------------------------------------------------

FROM ubuntu:20.04

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update && apt-get install -y \
    python3 \
    python3-pip \
    python3-venv \
    git \
    curl \
    ruby-full \
    vagrant \
    virtualbox \
    docker.io \
    docker-compose \
    sudo \
    mc \
    tree \
    nginx \
    php7.4 \
    php7.4-fpm \
    php7.4-mysql \
    php7.4-curl \
    php7.4-json \
    php7.4-mbstring \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

#--- Установка Slack CLI
RUN curl -fsSL https://downloads.slackapi.com/slack-cli/install.sh | bash



#-- Установка зависимостей Python
RUN python3 -m venv /opt/venv
ENV PATH="/opt/venv/bin:$PATH"

COPY requirements.txt /tmp/
RUN pip3 install -r /tmp/requirements.txt



#--- Установка гемов Ruby
RUN apt-get update && apt-get install -y libpq-dev postgresql-client libyaml-dev
RUN gem install bundler -v 2.4.22

COPY Gemfile /tmp/
WORKDIR /tmp
RUN bundle install



WORKDIR /app

RUN mkdir /app/shared_folder
VOLUME /app/shared_folder

CMD ["/bin/bash"]

