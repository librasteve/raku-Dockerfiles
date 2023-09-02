FROM librasteve/rakudo:scipy

LABEL maintainer="librasteve <librasteve@furnival.net>"
LABEL tag="librasteve/rakudo:ipyjk"

ENV PATH=$PATH:~/.cargo/bin
RUN curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | bash -s -- -y 

RUN    zef install https://github.com/niner/Inline-Python.git --exclude="python3"
RUN    zef install --/test Text::CSV
RUN    zef install git://github.com/bduggan/p6-jupyter-kernel.git
RUN    jupyter-kernel.raku --generate-config

#USER ${NB_UID}

ENTRYPOINT ["/bin/bash"]

#EXPOSE 8888
#CMD ["jupyter", "notebook", "--port=8888", "--no-browser", "--ip=0.0.0.0", "--allow-root"]
