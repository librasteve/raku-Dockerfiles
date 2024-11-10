FROM librasteve/rakudo:scipy

LABEL maintainer="librasteve <librasteve@furnival.net>"
LABEL tag="librasteve/rakudo:ipyjk"

ENV PATH=$PATH:~/.cargo/bin
RUN curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | bash -s -- -y 

RUN    export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:$(dirname $(which python))
ENV    LD_LIBRARY_PATH=$LD_LIBRARY_PATH:$(dirname $(which python))
RUN    zef install Inline::Python --exclude="python3" --/test
RUN    zef install --/test Text::CSV
RUN    zef install zef install 'Jupyter::Kernel:auth<zef:bduggan>' --verbose 
RUN    jupyter-kernel.raku --generate-config

#USER ${NB_UID}

ENTRYPOINT ["/bin/bash"]

#EXPOSE 8888
#CMD ["jupyter", "notebook", "--port=8888", "--no-browser", "--ip=0.0.0.0", "--allow-root"]
