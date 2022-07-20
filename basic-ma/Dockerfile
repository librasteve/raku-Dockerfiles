FROM ubuntu:latest
#covers arm64 and amd64 with buildx

LABEL maintainer="p6steve <p6steve@furnival.net>"
LABEL tag="p6steve/rakudo:basic"

ENV LANG=C.UTF-8 \
    LC_ALL=C.UTF-8 \
    TERM=xterm

ENV PATH=$PATH:/root/rakudo/bin:/root/rakudo/share/perl6/site/bin:/root/rakudo/share/perl6/vendor/bin:/root/rakudo/share/perl6/core/bin
      
RUN    apt-get update && apt-get upgrade -y \
    && apt-get install -y build-essential libssl-dev libreadline-dev git curl \
    && mkdir ~/rakudo && cd ~/rakudo \
    && curl -LJO https://rakudo.org/latest/star/src \
    && tar -xzf rakudo-star-*.tar.gz \
    && mv rakudo-star-*/* . && rm -fr rakudo-star-* \
    && ./bin/rstar install

RUN    zef install --/test Linenoise \
    && zef install App::Mi6 \
    && zef uninstall Readline

RUN apt-get install -y vim tree 

RUN echo ' \
set syntax=on\n \
set number\n \
set tabstop=4\n \
set shiftwidth=4\n \
set softtabstop=4\n \
set expandtab\n \
set autoindent\n \
set textwidth=127\n \
set fileformat=unix\n \
set fileencodings=utf-8\n \
set encoding=utf-8\n \
' >> ~/.vimrc

