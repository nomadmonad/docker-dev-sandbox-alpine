FROM ruby:3.2.2-alpine3.18

ENV ROOT="/rails_app"
ENV LANG=C.UTF-8
ENV TZ=Asia/Tokyo

WORKDIR ${ROOT}

RUN apk update && \
    apk upgrade && \
    apk add --no-cache \
    bash \
    vim \
    nodejs \
    mysql-dev \
    tzdata \
    yarn && \
    apk add --virtual build-packs --no-cache \
    alpine-sdk \
    build-base \
    curl-dev \
    mysql-client

COPY Gemfile ${ROOT}
COPY Gemfile.lock ${ROOT}

RUN gem install bundler:2.0.2 && \
    bundle install
RUN apk del build-packs

COPY . ${ROOT}

# Add a script to be executed every time the container starts.
COPY entrypoint.sh /usr/bin/
RUN chmod +x /usr/bin/entrypoint.sh
ENTRYPOINT ["entrypoint.sh"]
EXPOSE 3000

# Start the main process.
CMD ["rails", "server", "-b", "0.0.0.0"]
FROM ruby:3.2.2-alpine3.18

ENV ROOT="/rails_app"
ENV LANG=C.UTF-8
ENV TZ=Asia/Tokyo

WORKDIR "/rails_app"

RUN apk update && \
    apk upgrade && \
    apk add --no-cache \
    bash \
    nodejs \
    mysql-dev \
    tzdata \
    yarn && \
    apk add --virtual build-packs --no-cache \
    alpine-sdk \
    build-base \
    curl-dev \
    mysql-client

RUN pwd

COPY ./rails_app/Gemfile /rails_app/Gemfile
COPY ./rails_app/Gemfile.lock /rails_app/Gemfile.lock

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
