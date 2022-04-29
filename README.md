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
* stage-0: jupyter/scipy-notebook (ubuntu)   <=== supports both linux/arm64, linux/amd64
* stage-0.5: utilities (vi and so on)   [needed?]
* stage-1: rakudo from source                <=== no p6steve deps "p6steve/rakudo:scipynb-2022.02-arm64"
* stage-2: rakudan-ipydpaj                   <=== Inline::Python, Dan, Dan::Pandas "p6steve/raku-dan:pandas-2022.02-arm64"
* ...later...
* stage-2: rakudan-rncdpo                    <=== Rust NativeCall, Dan, Dan::Polars "p6steve/raku-dan:polars-2022.02-arm64"
* stage-2: rpm-emuj                          <=== Physics::Measure and deps (Physics::Unit, Physics::Error, Physics::Constants)
* stage-3: rpm-nyj                           <=== Physics::Navigation and Yacht::Navigation

Notes:
1. not sure can build polars on jupyter/scipy-notebook?? (so maybe stage-0 is pluggable with vanilla ubuntu)
2. hmmm maybe we have two stacks here (with / without jupyter)
