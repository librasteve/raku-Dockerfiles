FROM --platform=linux/arm64 p6steve/rakudo:ubuntu-latest-arm64 

ENV PATH=$PATH:~/.cargo/bin
ENV MVM_SPESH_DISABLE=1

RUN curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | bash -s -- -y 
