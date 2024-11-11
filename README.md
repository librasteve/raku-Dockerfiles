[![License: Artistic-2.0](https://img.shields.io/badge/License-Artistic%202.0-0298c3.svg)](https://opensource.org/licenses/Artistic-2.0)

[![rakudo:basic](https://github.com/librasteve/raku-Dockerfiles/actions/workflows/basic-ma-weekly.yaml/badge.svg)](https://github.com/librasteve/raku-Dockerfiles/actions/workflows/basic-ma-weekly.yaml)
[![rakudo:rusty](https://github.com/librasteve/raku-Dockerfiles/actions/workflows/rusty-ma-weekly.yaml/badge.svg)](https://github.com/librasteve/raku-Dockerfiles/actions/workflows/rusty-ma-weekly.yaml)
[![rakudo:scipy -> DH](https://github.com/librasteve/raku-Dockerfiles/actions/workflows/scipy-ma-weekly.yaml/badge.svg)](https://github.com/librasteve/raku-Dockerfiles/actions/workflows/scipy-ma-weekly.yaml)
[![rakudo:ipyjk -> DH](https://github.com/librasteve/raku-Dockerfiles/actions/workflows/ipyjk-ma-weekly.yaml/badge.svg)](https://github.com/librasteve/raku-Dockerfiles/actions/workflows/ipyjk-ma-weekly.yaml)

# raku-Dockerfiles
Common Dockerfiles for librasteve/raku modules (test and deploy)

Features:
* stacked
* run as CLI (default)
* easy start jupyter-notebook (local)
* covers --platform linux/arm64, linux/amd64
* combined with buildx as single image
* weekly latest to DockerHub
* implemented as GitHub Actions

Approach / naming:
| dir:         | from:                      | tag:                 | time:  | stack:  | layer: | platform:   |
|--------------|----------------------------|----------------------|--------|---------|--------|-------------|
| rakudo-basic | ubuntu:latest              | librasteve/rakudo:basic | 100min | rust    |    0   |  multiarch  |
| rakudo-rusty | librasteve/rakudo:basic       | librasteve/rakudo:rusty |   3min | rust    |    1   |  multiarch  |
| rakudo-scipy | jupyter/scipy-notebook:... | librasteve/rakudo:scipy |  19min | jupyter |    0   | multiarch4 |
| rakudo-ipyjk | librasteve/rakudo:scipy       | librasteve/rakudo:ipyjk |  15min | jupyter |    1   | multiarch |

Notes:
1. We have two stacks here ("rust" = ubuntu+rakudo+rust, "jupyter" = jupyter+rakudo+Inline::Python+rust)
2. Multi arch is [currently] linux/arm64,linux/amd64
3. Binder & Lightsail require amd64

# Docker Instructions

_following is "instructions to self" for manual build/run ... see GHA for the auto pipeline_

Client build ma on Docker Desktop:

* ```docker buildx build -t librasteve/rakudo:basic .```
* ```docker push librasteve/rakudo:basic```

Client run amd64 on M1 Docker Desktop:

* ```docker run -it -p 8888:8888 librasteve/rakudo:ipyjk```

[NB. --platform selector=linux/arm64 (or amd64) no longer needed, if used it MUST come BEFORE --port number!]

# Jupyter Instructions

* ```jupyter notebook --port=8888 --no-browser --allow-root --ip=0.0.0.0``` (for classic notebook)
* ```jupyter lab --port=8888 --no-browser --allow-root --ip=0.0.0.0``` (for console view)
* ```http://ubuntu:8888``` in browser (cut & paste token ID from CLI)

*DO NOT USE ALLOW ROOT IN A PRODUCTION SITE*

copyright(c) 2024 Henley Cloud Consulting Ltd.

