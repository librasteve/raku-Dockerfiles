[![License: Artistic-2.0](https://img.shields.io/badge/License-Artistic%202.0-0298c3.svg)](https://opensource.org/licenses/Artistic-2.0)

[![rakudo:basic](https://github.com/librasteve/raku-Dockerfiles/actions/workflows/basic-ma-weekly.yaml/badge.svg)](https://github.com/librasteve/raku-Dockerfiles/actions/workflows/basic-ma-weekly.yaml)
[![rakudo:rusty](https://github.com/librasteve/raku-Dockerfiles/actions/workflows/rusty-ma-weekly.yaml/badge.svg)](https://github.com/librasteve/raku-Dockerfiles/actions/workflows/rusty-ma-weekly.yaml)
[![rakudo:scipy](https://github.com/librasteve/raku-Dockerfiles/actions/workflows/scipy-weekly.yaml/badge.svg)](https://github.com/librasteve/raku-Dockerfiles/actions/workflows/scipy-weekly.yaml)
[![rakudo:ipyjk](https://github.com/librasteve/raku-Dockerfiles/actions/workflows/ipyjk-weekly.yaml/badge.svg)](https://github.com/librasteve/raku-Dockerfiles/actions/workflows/ipyjk-weekly.yaml)

# raku-Dockerfiles
Common Dockerfiles for librasteve/raku modules (test and deploy)

Features:
* stacked
* run as CLI (default)
* easy start jupyter-notebook (local)
* covers --platform linux/arm64, linux/amd64 (where possible)
* combined with buildx as single image
* weekly latest to DockerHub
* implemented as GitHub Actions

Approach / naming:
| dir:         | from:                      | tag:                 | time:  | stack:  | layer: | platform:   |
|--------------|----------------------------|----------------------|--------|---------|--------|-------------|
| rakudo-basic | ubuntu:latest              | librasteve/rakudo:basic | 100min | rust    |    0   |  multiarch  |
| rakudo-rusty | librasteve/rakudo:basic       | librasteve/rakudo:rusty |   3min | rust    |    1   |  multiarch  |
| rakudo-scipy | jupyter/scipy-notebook:... | librasteve/rakudo:scipy |  19min | jupyter |    0   | linux/amd64 |
| rakudo-ipyjk | librasteve/rakudo:scipy       | librasteve/rakudo:ipyjk |  15min | jupyter |    1   | linux/amd64 |

Notes:
1. We have two stacks here ("rust" = ubuntu+rakudo+rust, "jupyter" = jupyter+rakudo+Inline::Python+rust)
2. Multi arch is [currently] linux/arm64,linux/amd64
3. Binder requires FROM jupyter/scipy-notebook:xxx to have a tag (not 'latest')
4. Binder & Lightsail require amd64

# Docker Instructions

_following is "instructions to self" for manual build/run ... see GHA for the auto pipeline_

Client build arm64 on M1 vftools:

* ```docker build --no-cache -t librasteve/rakudo:scipynb .```
* ```docker push librasteve/rakudo:scipynb```

Client build amd64 on M1 Docker Desktop:

* ```docker build -t librasteve/raku-dan:pandas-amd64 --platform=linux/amd64 .```
* ```docker push librasteve/raku-dan:pandas-amd64```

Client run arm64 on M1 vftools:

* ```docker run -it -p 8888:8888 librasteve/raku-dan:pandas-arm64```
* ```docker ps```
* ```docker exec -it cont_name /bin/bash```

Client run amd64 on M1 Docker Desktop:

* ```docker run -it --platform linux/amd64 -p 8888:8888 librasteve/rakudo:ipyjk```
[NB. --platform selector MUST come BEFORE --port number!]

# Jupyter Instructions

* ```jupyter notebook --port=8888 --no-browser --allow-root --ip=0.0.0.0``` (for classic notebook)
* ```jupyter lab --port=8888 --no-browser --allow-root --ip=0.0.0.0``` (for console view)
* ```http://ubuntu:8888``` in browser (cut & paste token ID from CLI)

copyright(c) 2024 Henley Cloud Consulting Ltd.

