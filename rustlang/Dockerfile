FROM ubuntu:xenial-20170619

ENV USER root
ENV DEBIAN_FRONTEND=noninteractive
ENV RUST_VERSION=1.18.0

RUN apt-get update && \
    apt-get install -y --no-install-recommends \
       build-essential \
       git \
       curl \
       libssl-dev \
       ca-certificates \
       openssh-client \
       pkg-config && \
  curl -sO https://static.rust-lang.org/dist/rust-$RUST_VERSION-x86_64-unknown-linux-gnu.tar.gz && \
  tar -xzf rust-$RUST_VERSION-x86_64-unknown-linux-gnu.tar.gz && \
  ./rust-$RUST_VERSION-x86_64-unknown-linux-gnu/install.sh --without=rust-docs && \
  apt remove --purge -y curl && \
  apt autoremove -y && \
  rm -rf \
    rust-$RUST_VERSION-x86_64-unknown-linux-gnu \
    rust-$RUST_VERSION-x86_64-unknown-linux-gnu.tar.gz \
    /var/lib/apt/lists/* \
    /tmp/* \
    /var/tmp/* && \
  mkdir /source
VOLUME ["/source"]
WORKDIR /source
CMD ["/bin/bash"]
