FROM phusion/baseimage:0.9.19

RUN apt-get update && \
    apt-get install -y npm \
        mysql-client \
        sqlite3 \
        iputils-ping && \
    npm install -g n

##
## Timezone
##

ARG TZ=UTC
ENV TZ ${TZ}
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

##
## Node
##

ARG NODE_VERSION=latest
ENV NODE_VERSION=$NODE_VERSION

# Install the specified NODE_VERSION or grab latest
RUN n "$NODE_VERSION"

ARG YARN=true
ARG NEST=true
ARG NEST_VERSION=9

ENV YARN=$YARN
ENV NEST=$NEST
ENV NEST_VERSION=$NEST_VERSION

# Install YARN && NEST
RUN if [ ${YARN} = true ]; then \
    npm install -g yarn \
;fi
RUN if [ ${NEST} = true ]; then \
    yarn global add @nestjs/cli@$NEST_VERSION \
;fi

##
## Cron
##

COPY ./crontab /var/spool/cron/crontabs
COPY package*.json ./

WORKDIR /opt/app

ENTRYPOINT sleep infinity