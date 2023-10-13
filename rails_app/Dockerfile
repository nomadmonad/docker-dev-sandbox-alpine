FROM ruby:3.2.2-alpine3.18

ENV ROOT="/app"
ENV LANG=C.UTF-8
ENV TZ=Asia/Tokyo

WORKDIR ${ROOT}

RUN apk update && \
    apk upgrade && \
    apk add --no-cache \
    linux-headers \
    libxml2-dev \
    make \
    gcc \
    libc-dev \
    bash \
    vim \
    git \
    nodejs \
    mysql-dev \
    tzdata \
    yarn && \
    apk add --virtual build-packs --no-cache \
    alpine-sdk \
    build-base \
    curl-dev \
    mysql-client

COPY Gemfile Gemfile.lock ${ROOT}

RUN gem install bundler:2.4.1 && \
    bundle install
RUN apk del build-packs

# COPY . ${ROOT}

# Add a script to be executed every time the container starts.
COPY entrypoint.sh /usr/bin/
RUN chmod +x /usr/bin/entrypoint.sh
ENTRYPOINT ["entrypoint.sh"]
EXPOSE 3000

# Start the main process.
CMD ["rails", "server", "-b", "0.0.0.0"]
