![Oxford Nanopore Technologies logo](images/ONT_logo_590x106.png)

Pomoxis - bioinformatics tools for nanopore research 
====================================================

[![Build Status](https://travis-ci.org/nanoporetech/pomoxis.svg?branch=master)](https://travis-ci.org/nanoporetech/pomoxis)

Pomoxis comprises a set of basic bioinformatic tools tailored to nanopore
sequencing. Notably tools are included for generating and analysing draft
assemblies. Many of these tools are used by the research data analysis
group at Oxford Nanopore Technologies.

Documentation can be found at https://nanoporetech.github.io/pomoxis/.

© 2018 Oxford Nanopore Technologies Ltd.

Features
--------

 * Wraps third party tools with known good default parameters
   and methods of use.
 * Creates an isolated environment with all third-party tools.
 * Can be installed with conda.
 * Streamlines common short analysis chains.
 * Includes a nanopore read simulator.
 * Server/client components for minimap2 and bwa.
 * Integrates into [katuali](https://github.com/nanoporetech/katuali)
   for performing more complex analysis pipelines.
 * Open source (Mozilla Public License 2.0).


Compatibility
-------------

Pomoxis is developed on Ubuntu 16.04, other recent linuxes should be
equally compatible (see build notes below). Pomoxis is known to work on
at least some MacOS High Sierra configurations, though some components,
notably scrappy, are known to not work on some MacOS configurations
(combinations of OS and xcode versions).


Installation
------------

Much of pomoxis's functionality is dependent on thirty party tools. These
can be provided by the user, or can be installed with the help of the
provided `Makefile`

**Installation with conda**

Pomoxis can be installed using the [conda](https://conda.io/docs/) package
manager. Many users will prefer this method. If `make` is installed on the
system, the following will create a conda environment and install pomoxis
and its third party dependencies into the environment:

    git clone --recursive https://github.com/nanoporetech/pomoxis
    cd pomoxis
    CONDA=<path to conda install> make conda

On the final line, use for example:

    CONDA=~/miniconda3/ make conda

A conda package is planned in the future.


**Installation from source**

With this method pomoxis will install itself into a an isolated virtual
environment. The installation will fetch, compile, and install all direct
dependencies into the environment. Use this method if you do not wish to
use conda, but will not be providing the third-party binaries.

> Before installing pomoxis is may be required to install some prerequisite
> packages, best installed by a package manager. On Ubuntu these are:
> * gcc-4.9
> * g++-4.9
> * zlib1g-dev
> * libncurses5-dev
> * python3-all-dev
> * libhdf5-dev
> * libatlas-base-dev
> * libopenblas-base
> * libopenblas-dev
> * libbz2-dev
> * liblzma-dev
> * libffi-dev
> * make
> * python-virtualenv
> * cmake (for racon)
> * wget (for fetching modules from github)
> * bzip2 (for extracting those modules)

To setup the environment run:

    git clone --recursive https://github.com/nanoporetech/pomoxis
    cd pomoxis
    make install
    . ./venv/bin/activate
    

The installation of porechop (https://github.com/rrwick/Porechop)
requires a newer compiler than is a available on some systems. It may therefore
be necessary to install a newer compiler and set environment variables before
the `make install` step:

    # For porechop to be compiled on older systems set these, e.g.:
    export CXX="g++-4.9" CC="gcc-4.9"

Note also that racon requires at least `gcc>=4.8.5` to
[compile smoothly](https://github.com/isovic/racon/issues/57).


**Installation without compiling third-party binaries**

Running the above within a pre-exisiting (virtual) environnment may well fail;
advanced may wish to simply run

    python setup.py install

in the standard manner after compiling the third party programs listed below
and ensuring they are present on the `PATH`. The `setup.py` script can copy
the binaries into the python interpreter path if they are placed within a
directory named `bincache` alongside `setup.py`. To make use of this facility
run:

    pip install -r requirements.txt
    POMO_BINARIES=1 python setup.py install


Third party binaries
--------------------

The distribution bundles some common bioinformatics tools:

* miniasm
* minimap2
* racon
* samtools
* bcftools
* seqkit
* porechop

Help
----

**Licence and Copyright**

© 2018 Oxford Nanopore Technologies Ltd.

`pomoxis` is distributed under the terms of the Mozilla Public License 2.0.

**Research Release**

Research releases are provided as technology demonstrators to provide early
access to features or stimulate Community development of tools. Support for
this software will be minimal and is only provided directly by the developers.
Feature requests, improvements, and discussions are welcome and can be
implemented by forking and pull requests. However much as we would
like to rectify every issue and piece of feedback users may have, the 
developers may have limited resource for support of this software. Research
releases may be unstable and subject to rapid iteration by Oxford Nanopore
Technologies.
