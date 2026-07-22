FROM ubuntu:26.04@sha256:3131b4cc82a783df6c9df078f86e01819a13594b865c2cad47bd1bca2b7063bb
ARG DEBIAN_FRONTEND=noninteractive
RUN apt-get update && \
    apt-get install --no-install-recommends -y \
        automake \
        autoconf \
        bison \
        build-essential \
        bzip2 \
        cmake \
        curl \
        flex \
        gfortran \
        git \
        libaec-dev \
        libcurl4-openssl-dev \
        libjpeg-dev \
        libopenmpi-dev \
        libx11-dev \
        libzip-dev \
        m4 \
        openmpi-bin \
	python3.10 \
        python3-dev \
        python3-mpi4py \
        python3-numpy \
        python3-pip \
        wget \
        zlib1g-dev && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*
RUN update-alternatives --install /usr/bin/python python /usr/bin/python3.12 1
RUN git clone --depth 1 https://github.com/sandialabs/seacas.git
WORKDIR /seacas
RUN ./install-tpl.sh
RUN mkdir build
WORKDIR /seacas/build
RUN ../cmake-exodus && \
    make && \
    make install
ENV PATH="${PATH}:/seacas/bin/"
CMD ["/bin/bash"]
