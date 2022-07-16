[![License: Artistic-2.0](https://img.shields.io/badge/License-Artistic%202.0-0298c3.svg)](https://opensource.org/licenses/Artistic-2.0)

# raku-Dockerfiles
Common Dockerfiles for p6steve/raku modules (test and deploy)

Requirements:
* staged
* run as CLI (default)
* easy start jupyter-notebook (local)
* binder compatible (if possible)
* cover --platform linux/arm64, linux/amd64
* combine with buildx as single ditro (later)
* stacked, but limit branches
* can be implemented as GH actions (later)

Approach / naming:
* rakudo-basic	ubuntu:latest => p6steve/rakudo:basic
* rakudo-rusty	p6steve/rakudo:basic => p6steve/rakudo:rusty
* rakudo-scipy	jupyter/scipy-notebook:... => p6steve/rakudo:scipy
* rakudo-ipyjk	p6steve/rakudo:scipy => p6steve/rakudo:ipyjk

Notes:
1. not sure can build polars on jupyter/scipy-notebook?? (so maybe stage-0 is pluggable with vanilla ubuntu)
2. hmmm maybe we have two stacks here (with / without jupyter)
3. Binder requires  FROM jupyter/scipy-notebook to have a tag (not 'latest') - may need to parameterize

# Docker Instructions

Client build arm64 on M1 vftools:

* ```docker build --no-cache -t p6steve/rakudo:scipynb-2022.02-arm64 .```
* ```docker push p6steve/rakudo:scipynb-2022.02-arm64```

Client build amd64 on M1 Docker Desktop:

Client run:

* ```docker run -it -p 8888:8888 p6steve/raku-dan:pandas-2022.02-arm64```
* ```docker ps```
* ```docker exec -it cont_name /bin/bash```

# Jupyter Instructions

* ```jupyter notebook --port=8888 --no-browser --allow-root --ip=0.0.0.0```
* ```http://ubuntu:8888``` in browser

copyright(c) 2022 Henley Cloud Consulting Ltd.

