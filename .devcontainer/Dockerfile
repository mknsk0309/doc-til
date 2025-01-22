FROM node:alpine

ARG ENV_USERNAME
ARG ENV_WORKDIR

ENV LANG C.UTF-8
ENV TZ Asia/Tokyo

RUN apk update && apk add --no-cache git bash sudo tzdata python3

RUN adduser -D ${ENV_USERNAME} \
  && mkdir -p ${ENV_WORKDIR}/node_modules \
  && chown -R ${ENV_USERNAME}:${ENV_USERNAME} ${ENV_WORKDIR}/node_modules \
  && mkdir -p ${ENV_WORKDIR}/venv \
  && chown -R ${ENV_USERNAME}:${ENV_USERNAME} ${ENV_WORKDIR}/venv \
  && echo ${ENV_USERNAME} "ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers

WORKDIR ${ENV_WORKDIR}
USER ${ENV_USERNAME}

RUN python3 -m venv venv 
RUN source venv/bin/activate \
  && pip install --upgrade pip \
  && pip install --upgrade mkdocs mkdocs-material

COPY package.json yarn.lock ${ENV_WORKDIR}/
RUN yarn install
