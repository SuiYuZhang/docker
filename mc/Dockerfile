FROM tensorflow/tensorflow:1.12.0

# Switch to aliyun sources
COPY ubuntu_16.04_aliyun.sources.list /etc/apt/sources.list

# GPG keys are broken
# RUN mv /etc/apt/sources.list.d/cuda.list /etc/apt/sources.list.d/cuda.list.bak
# RUN mv /etc/apt/sources.list.d/nvidia-ml.list /etc/apt/sources.list.d/nvidia-ml.list.bak

RUN apt-get update -y && \
    apt-get install -y --no-install-recommends \
    apt-utils \
    && rm -rf /var/lib/apt/lists/*

# Setup vim
RUN apt-get update -y && \
    apt-get install -y --no-install-recommends \
    apt-utils \
    locales \
    vim \
    && rm -rf /var/lib/apt/lists/*

RUN locale-gen en_US.UTF-8
ENV LC_CTYPE=en_US.UTF-8
ENV LC_ALL=en_US.UTF-8
ENV TERM xterm-256color

# Install essential tools
RUN apt-get update -y && \
    apt-get install -y --no-install-recommends \
    pkg-config \
    software-properties-common \
    curl \
    git \
    less \
    unzip \
    zip \
    wget \
    rsync \
    telnet \
    screen \
    tmux \
    openssh-server \
    bsdmainutils \
    && rm -rf /var/lib/apt/lists/*

# Install monitor tools
RUN apt-get update -y && \
    apt-get install -y --no-install-recommends \
    htop \
    strace \
    pstack \
    sysstat \
    dstat \
    lsof \
    iotop \
    net-tools \
    inetutils-ping \
    iftop \
    tcpdump \
    inetutils-traceroute \
    pciutils \
    && rm -rf /var/lib/apt/lists/*

# Install build tools
RUN apt-get update -y && \
    apt-get install -y --no-install-recommends \
    build-essential \
    make \
    ninja-build \
    automake \
    autoconf \
    autoconf-archive \
    libtool \
    cmake \
    ccache \
    gcovr \
    && rm -rf /var/lib/apt/lists/*

# Upgrade CMake
ENV CMAKE_VERSION 3.16.2
RUN wget -p -O cmake.tar.gz https://github.com/Kitware/CMake/releases/download/v${CMAKE_VERSION}/cmake-${CMAKE_VERSION}-Linux-x86_64.tar.gz && \
    tar zxf cmake.tar.gz --strip-components=1 -C /usr/local/ && \
    update-alternatives --install /usr/bin/cmake cmake /usr/local/bin/cmake 1 --force && \
    rm -f cmake.tar.gz

# Setup VIM
# RUN git clone --recursive https://github.com/llhe/vimrc.git
# RUN rm -rf ~/.vim
# RUN rm -rf ~/.vimrc
# RUN ln -s `pwd`/vimrc/vim ~/.vim
# RUN ln -s `pwd`/vimrc/vimrc ~/.vimrc

# Install python
RUN apt-get update -y && \
    apt-get install -y --no-install-recommends \
    python-pip \
    python2.7 \
    python2.7-dev \
    && rm -rf /var/lib/apt/lists/*

RUN echo 'alias python=python2' >> ~/.bashrc

RUN pip config --user set global.index http://mirrors.aliyun.com/pypi/simple
RUN pip config --user set global.index-url http://mirrors.aliyun.com/pypi/simple
RUN pip config --user set global.trusted-host mirrors.aliyun.com
RUN pip install --upgrade pip

RUN pip install \
    wheel==0.36.1 \
    setuptools==44.0.0

# Install Python packages
RUN pip install \
    clang-format==9.0.0 \
    pycodestyle==2.5.0 \
    yapf==0.28.0 \
    cpplint==1.4.4 \
    future==0.18.2 \
    protobuf==3.11.3 \
    wheel==0.36.1 \
    virtualenv==20.0.30 \
    matplotlib==2.2.5 \
    pillow==6.2.1 \
    scipy==1.2.1 

# Install devel libs
RUN apt-get update -y && \
    apt-get install -y --no-install-recommends \
    libssl-dev \
    zlib1g-dev \
    libcurl3-dev \
    libboost-all-dev \
    libgoogle-glog-dev \
    libprotobuf-dev \
    protobuf-compiler \
    libprotoc-dev \
    && rm -rf /var/lib/apt/lists/*
