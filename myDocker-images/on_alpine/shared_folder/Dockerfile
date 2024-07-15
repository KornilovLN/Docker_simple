#---------------------------------------------------------------------------------------------
# Образ базового контейнера на alpine для создания остальных докер-сервисов 
#
# Команда создания базового образа:  
# docker build -t base_myalpine_image .
#
# Команда запуска для интерактивного режима
# docker run -it --rm -v ~/virt/dockers/on_alpine/shared_folder:/app/shared_folder base_myalpine_image
#---------------------------------------------------------------------------------------------

FROM alpine:3.18

ENV DEBIAN_FRONTEND=noninteractive

RUN echo "http://dl-cdn.alpinelinux.org/alpine/v3.18/community" >> /etc/apk/repositories

RUN apk update && apk add --no-cache \
    python3 \
    py3-pip \
    git \
    curl \
    ruby \
    vim \
    nano \
    tree \
    sudo \
    nginx \
    php81 \
    php81-fpm \
    php81-mysqli \
    php81-curl \
    php81-json \
    php81-mbstring \
    mc \
    docker \
    docker-compose \
    && rm -rf /var/cache/apk/*



RUN apk add --no-cache gcc g++ gfortran build-base python3-dev openblas-dev lapack-dev

#-- Установка зависимостей Python
RUN python3 -m venv /opt/venv
ENV PATH="/opt/venv/bin:$PATH"

COPY requirements.txt /tmp/
RUN pip install --no-cache-dir --upgrade pip
RUN pip install --no-cache-dir --only-binary=numpy,pandas -r /tmp/requirements.txt
RUN pip install -r /tmp/requirements.txt

WORKDIR /app

RUN mkdir /app/shared_folder
VOLUME /app/shared_folder

CMD ["/bin/sh"]

