FROM ubuntu:14.04

MAINTAINER Alejandro Torres <fulgorek@gmail.com>

ARG RUBY_VERSION

ENV RUBY_VERSION=${RUBY_VERSION:-2.3.0}

# Install ruby dependencies
RUN apt-get update && \
    apt-get upgrade -y && \
    apt-get install -y wget \
                       curl \
                       build-essential \
                       git git-core \
                       zlib1g-dev \
                       libssl-dev \
                       libreadline-dev \
                       libyaml-dev \
                       libsqlite3-dev \
                       sqlite3 \
                       libxml2-dev \
                       libxslt1-dev \
                       gawk \
                       autoconf \
                       libgmp-dev \
                       libgdbm-dev \
                       libncurses5-dev \
                       automake \
                       libtool \
                       bison \
                       pkg-config \
                       libffi-dev

# Cleanups
RUN apt-get autoremove -y && \
    apt-get clean

# Install ruby-install
RUN cd /tmp && \
    gpg --keyserver hkp://keys.gnupg.net --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3 && \
    curl -sSL https://get.rvm.io | bash -s stable && \
    /bin/bash -l -c "source /etc/profile.d/rvm.sh" && \
    /bin/bash -l -c "rvm install $RUBY_VERSION" && \
    echo "source /etc/profile.d/rvm.sh" >> ~/.bashrc

# Add options to gemrc
RUN echo "gem: --no-rdoc --no-ri" > ~/.gemrc

# Install bundler
RUN gem install bundler

