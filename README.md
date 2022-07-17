[![rakudo:basic-ma -> DH](https://github.com/p6steve/raku-Dockerfiles/actions/workflows/basic-ma-weekly.yaml/badge.svg)](https://github.com/p6steve/raku-Dockerfiles/actions/workflows/basic-ma-weekly.yaml)
[![rakudo:rusty-ma -> DH](https://github.com/p6steve/raku-Dockerfiles/actions/workflows/rusty-ma-weekly.yaml/badge.svg)](https://github.com/p6steve/raku-Dockerfiles/actions/workflows/rusty-ma-weekly.yaml)
[![rakudo:scipy-ma -> DH](https://github.com/p6steve/raku-Dockerfiles/actions/workflows/scipy-ma-weekly.yaml/badge.svg)](https://github.com/p6steve/raku-Dockerfiles/actions/workflows/scipy-ma-weekly.yaml)
[![rakudo:ipyjk-ma -> DH](https://github.com/p6steve/raku-Dockerfiles/actions/workflows/ipyjk-ma-weekly.yaml/badge.svg)](https://github.com/p6steve/raku-Dockerfiles/actions/workflows/ipyjk-ma-weekly.yaml)

# TODOs
- [ ] rakudo:scipy
- [ ] rakudo:ipyjk

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
| dir:         | from:                      | tag:                 | time:  |
|--------------|----------------------------|----------------------|--------|
| rakudo-basic | ubuntu:latest              | p6steve/rakudo:basic | 100min |
| rakudo-rusty | p6steve/rakudo:basic       | p6steve/rakudo:rusty |   3min |
| rakudo-scipy | jupyter/scipy-notebook:... | p6steve/rakudo:scipy |  |
| rakudo-ipyjk | p6steve/rakudo:scipy       | p6steve/rakudo:ipyjk |  |

Notes:
1. We have two stacks here (ubuntu+rakudo+rust, jupyter+rakudo+Inline::Python)
1. Binder requires  FROM jupyter/scipy-notebook to have a tag (not 'latest') - may need to parameterize

# GH Actions

Each Dockerfile has a weekly build GitHub Action that pushes the latest image to Docker Hub. These take ~85 mins each (!) to run. You can go much faster on a laptop.

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

[![License: Artistic-2.0](https://img.shields.io/badge/License-Artistic%202.0-0298c3.svg)](https://opensource.org/licenses/Artistic-2.0
copyright(c) 2022 Henley Cloud Consulting Ltd.

