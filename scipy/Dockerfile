FROM jupyter/scipy-notebook:latest
#must have tag for Binder (not 'latest')
#covers amd64 only 

LABEL maintainer="p6steve <p6steve@furnival.net>"
LABEL tag="p6steve/rakudo:basic"

ENV PATH=$PATH:/usr/share/perl6/site/bin

USER root

RUN buildDeps="libc6-dev libencode-perl libzstd-dev libssl-dev \
               libbz2-dev libreadline-dev libsqlite3-dev llvm \
               libncurses5-dev tk-dev liblzma-dev \
               python-openssl python3-dev libpython3.9-dev" \
    && apt-get update && apt-get upgrade -y \
    && apt-get install -y --no-install-recommends build-essential curl wget $buildDeps

RUN mkdir ~/rakudo && cd ~/rakudo \
    && curl -LJO https://rakudo.org/latest/star/src \
    && tar -xzf rakudo-star-*.tar.gz \
    && mv rakudo-star-*/* . && rm -fr rakudo-star-* \
    && ./bin/rstar install

RUN zef install Linenoise App::Mi6 App::Prove6 \
    && zef uninstall Readline

#USER ${NB_UID}

ENTRYPOINT ["/bin/bash"]

#EXPOSE 8888
#CMD ["jupyter", "notebook", "--port=8888", "--no-browser", "--ip=0.0.0.0", "--allow-root"]
