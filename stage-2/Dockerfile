FROM p6steve/rakudo:scipynb-2022.02-arm64

RUN zef install https://github.com/niner/Inline-Python.git --exclude="python3" \
    && zef -v install git://github.com/bduggan/p6-jupyter-kernel.git \
    && jupyter-kernel.raku --generate-config

#USER ${NB_UID}

ENTRYPOINT ["/bin/bash"]

#EXPOSE 8888
#CMD ["jupyter", "notebook", "--port=8888", "--no-browser", "--ip=0.0.0.0", "--allow-root"]
