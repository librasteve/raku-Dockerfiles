FROM p6steve/rakudo:ipyjk-2022.02-arm64

USER root

RUN    zef install Text::CSV \
    && zef install https://github.com/p6steve/raku-dan.git \
    && zef install https://github.com/p6steve/raku-dan-pandas.git \
    && git clone https://github.com/p6steve/raku-Dan-Jupyter.git \
    && cp -R raku-Dan-Jupyter/eg ${HOME}

#USER ${NB_UID}

ENTRYPOINT ["/bin/bash"]

#EXPOSE 8888
#CMD ["jupyter", "notebook", "--port=8888", "--no-browser", "--ip=0.0.0.0", "--allow-root"]
