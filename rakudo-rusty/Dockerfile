FROM --platform=linux/arm64 p6steve/rakudo:basic

LABEL maintainer="p6steve <p6steve@furnival.net>"
LABEL tag="p6steve/rakudo:rusty"

ENV PATH=$PATH:~/.cargo/bin

RUN curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | bash -s -- -y 
