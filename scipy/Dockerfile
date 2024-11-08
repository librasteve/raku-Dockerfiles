FROM jupyter/scipy-notebook:latest

LABEL maintainer="librasteve <librasteve@furnival.net>"
LABEL tag="librasteve/rakudo:scipy"

USER root

RUN buildDeps="libc6-dev libencode-perl libzstd-dev libssl-dev \
               libbz2-dev libreadline-dev libsqlite3-dev llvm \
               libncurses5-dev tk-dev liblzma-dev \
               python3-openssl python3-dev libpython3.10-dev" \
    && apt-get update && apt-get upgrade -y \
    && apt-get install -y --no-install-recommends build-essential curl wget $buildDeps \
    && rm -rf /var/lib/apt/lists/* 

ENV LANG=C.UTF-8 \
    LC_ALL=C.UTF-8 \
    TERM=xterm

ENV PATH=$PATH:$HOME/rakudo/bin:$HOME/rakudo/share/perl6/site/bin:$HOME/rakudo/share/perl6/vendor/bin:$HOME/rakudo/share/perl6/core/bin

RUN    apt-get update && apt-get upgrade -y \
    && apt-get install -y build-essential libssl-dev libreadline-dev git curl \
    && mkdir ~/rakudo && cd ~/rakudo \
    && curl -LJO https://rakudo.org/latest/star/src \
    && tar -xzf rakudo-star-*.tar.gz \
    && mv rakudo-star-*/* . && rm -fr rakudo-star-* \
    && ./bin/rstar install

RUN zef install Linenoise App::Mi6 && zef uninstall Readline

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
set foldmethod=indent\n \
set foldnestmax=10\n \
set nofoldenable\n \
set foldlevel=2\n \
' >> ~/.vimrc

#USER ${NB_UID}

ENTRYPOINT ["/bin/bash"]

#EXPOSE 8888
#CMD ["jupyter", "notebook", "--port=8888", "--no-browser", "--ip=0.0.0.0", "--allow-root"]
