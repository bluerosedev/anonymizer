FROM ruby:2.4

MAINTAINER Mateusz Koszutowski <mkoszutowski@divante.pl>

WORKDIR /usr/src/anonymizer

ARG UID=1000
ARG GID=1000

USER root

RUN apt-get update \
    && apt-get install -y \
        mysql-client \
        rsync \
        build-essential \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

# Create anonymizer user
RUN if [ ! `id -g anonymizer &> /dev/null` ]; then groupadd -f -g ${GID} anonymizer; fi \
    && if [ ! `id -u anonymizer &> /dev/null` ]; then useradd --shell /bin/bash -u ${UID} -g ${GID} -m anonymizer; fi

COPY . .

RUN chown -R anonymizer:anonymizer .

USER anonymizer

RUN bundle install --deployment --force
