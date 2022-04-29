FROM jupyter/scipy-notebook:4b830d5897d8
#must have tag for Binder (not 'latest')

ENV PATH=$PATH:/usr/share/perl6/site/bin

USER root

RUN buildDeps="libc6-dev libencode-perl libzstd-dev libssl-dev \
               libbz2-dev libreadline-dev libsqlite3-dev llvm \
               libncurses5-dev tk-dev liblzma-dev \
               python-openssl python3-dev libpython3.9-dev" \
    && apt-get update && apt-get upgrade -y \
    && apt-get install -y --no-install-recommends build-essential curl wget $buildDeps \
    && rm -rf /var/lib/apt/lists/* 

RUN mkdir rakudo \
    && wget -O rakudo.tar.gz https://github.com/rakudo/rakudo/releases/download/2022.02/rakudo-2022.02.tar.gz \
    && tar xzf rakudo.tar.gz --strip-components=1 -C rakudo \
    && ( \ 
        cd rakudo && git init \
        && perl Configure.pl --prefix=/usr --gen-moar --gen-nqp \
        --backends=moar --moar-option='--toolchain=gnu' --relocatable \
        && make && make install \
    ) \ 
    && rm -rf rakudo rakudo.tar.gz \
    && git clone -b master --single-branch https://github.com/ugexe/zef.git \
    && cd zef && raku -I. bin/zef install . \
    && cd ..  && rm -rf zef \
    && zef install Linenoise App::Mi6 App::Prove6

#USER ${NB_UID}

ENTRYPOINT ["/bin/bash"]

#EXPOSE 8888
#CMD ["jupyter", "notebook", "--port=8888", "--no-browser", "--ip=0.0.0.0", "--allow-root"]
