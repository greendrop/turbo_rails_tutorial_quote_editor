FROM node:18.15.0-bullseye-slim as node
FROM ruby:3.2.1-slim-bullseye

COPY --from=node /opt/ /opt/
COPY --from=node /usr/local/lib/node_modules /usr/local/lib/node_modules
COPY --from=node /usr/local/bin/node /usr/local/bin/node
RUN cd /usr/local/bin \
  && ln -s /usr/local/bin/node nodejs \
  && ln -s ../lib/node_modules/npm/bin/npm-cli.js npm \
  && ln -s ../lib/node_modules/npm/bin/npx-cli.js npx \
  && ln -s /opt/yarn-v1.22.19/bin/yarn yarn \
  && ln -s /opt/yarn-v1.22.19/bin/yarnpkg yarnpkg

RUN set -ex \
  && apt-get update \
  && apt-get upgrade -y \
  && apt-get install -y --no-install-recommends \
  iputils-ping locales task-japanese gosu sudo vim less zsh \
  build-essential patch ruby-dev zlib1g-dev liblzma-dev \
  libpq-dev \
  python3 graphviz \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/* \
  && echo 'ja_JP.UTF-8 UTF-8' > /etc/locale.gen \
  && locale-gen \
  && update-locale LANG=ja_JP.UTF-8 \
  && cp -p /usr/share/zoneinfo/Asia/Tokyo /etc/localtime
ENV LANG ja_JP.UTF-8
