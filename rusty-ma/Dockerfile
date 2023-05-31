FROM librasteve/rakudo:basic

LABEL maintainer="librasteve<librasteve@furnival.net>"
LABEL tag="librasteve/rakudo:rusty"

ENV PATH=$PATH:~/.cargo/bin

RUN curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | bash -s -- -y 
