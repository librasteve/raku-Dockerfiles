FROM --platform=linux/arm64 ubuntu:latest

ENV LANG=C.UTF-8 \
    LC_ALL=C.UTF-8 \
    TERM=xterm \
    RAKUDO=2022.02

ENV PATH=$PATH:/usr/share/perl6/site/bin

LABEL maintainer="p6steve <p6steve@furnival.net>"
      
RUN buildDeps="gcc \
        libc6-dev \
        libencode-perl \
        wget \
        libzstd-dev \
        make" \
    && apt-get update && apt-get upgrade -y \
    && apt-get install -y --no-install-recommends $buildDeps \
    && apt-get install -y git nano curl vim libssl-dev \
    && rm -rf /var/lib/apt/lists/* \
    && mkdir rakudo && git init \
    && wget -O rakudo.tar.gz https://github.com/rakudo/rakudo/releases/download/${RAKUDO}/rakudo-${RAKUDO}.tar.gz \
    && tar xzf rakudo.tar.gz --strip-components=1 -C rakudo \
    && ( \
        cd rakudo \
        && perl Configure.pl --prefix=/usr --gen-moar --gen-nqp \
        --backends=moar --moar-option='--toolchain=gnu' --relocatable \
        && make && make install \
    ) \
    && rm -rf rakudo rakudo.tar.gz \
    && git clone -b master --single-branch https://github.com/ugexe/zef.git \
    && cd zef \
    && raku -I. bin/zef install . && cd .. && rm -rf zef \
    && zef install Linenoise App::Mi6 App::Prove6 \
    && zef install JSON::Tiny Digest::HMAC Digest::SHA256::Native
    #&& apt-get purge -y --auto-remove $buildDeps

RUN echo ' \ 
set syntax=on\n \
set number\n \
set tabstop=4\n \
set shiftwidth=4\n \
set softtabstop=4\n \
set expandtab\n \
set autoindent\n \
set textwidth=79\n \
set fileformat=unix\n \
set fileencodings=utf-8\n \
set encoding=utf-8\n \
' >> ~/.vimrc
    
#CMD ["raku", "--version"]
