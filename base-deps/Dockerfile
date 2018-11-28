# The base-deps Docker image installs main libraries needed to run Ray Cluster
# Include java and hadoop
FROM ubuntu:18.04

RUN mkdir -p /usr/local/java \
 && mkdir -p /usr/local/hadoop

ENV JAVA_VERSION=8u191
ENV JAVA_DIR=jdk1.8.0_191
ENV HADOOP_VERSION=3.1.1

COPY ./jdk-${JAVA_VERSION}-linux-x64.tar.gz /tmp
COPY ./hadoop-${HADOOP_VERSION}.tar.gz /tmp
COPY ./.vimrc /root

RUN apt-get update \
    && apt-get install -y \
        git \
        wget \
        cmake \
        pkg-config \
        build-essential \
        autoconf \
        curl \
        libtool \
        unzip \
        flex \
        bison \
        maven \
        vim \
    && apt-get clean \
    && echo 'export PATH=/opt/conda/bin:$PATH' > /etc/profile.d/conda.sh \
    && wget \
        --quiet 'https://repo.continuum.io/archive/Anaconda2-5.2.0-Linux-x86_64.sh' \
        -O /tmp/anaconda.sh \
    && /bin/bash /tmp/anaconda.sh -b -p /opt/conda \
    && rm /tmp/anaconda.sh \
    && /opt/conda/bin/conda install -y \
        libgcc \
    && /opt/conda/bin/conda clean -y --all \
    && /opt/conda/bin/pip install --upgrade pip \
    && /opt/conda/bin/pip install \
        flatbuffers \
        cython==0.27.3

RUN tar -zxvf /tmp/jdk-${JAVA_VERSION}-linux-x64.tar.gz -C /tmp \
 && cp -rf /tmp/${JAVA_DIR}/* /usr/local/java \
 && rm -rf /tmp/${JAVA_DIR} && rm -rf /tmp/jdk-${JAVA_VERSION}-linux64.tar.gz \
 && tar -zxvf /tmp/hadoop-${HADOOP_VERSION}.tar.gz -C /tmp \
 && cp -rf /tmp/hadoop-${HADOOP_VERSION}/* /usr/local/hadoop \
 && rm -rf /tmp/hadoop-${HADOOP_VERSION} && rm -rf /tmp/hadoop-${HADOOP_VERSION}

ENV JAVA_HOME "/usr/local/java"
ENV CLASS_PATH "${JAVA_HOME}/jre/lib:${JAVA_HOME}/lib"
ENV HADOOP_HOME "/usr/local/hadoop"
ENV HADOOP_CONF_DIR "${HADOOP_HOME}/etc/hadoop" 
ENV PATH "/opt/conda/bin:${JAVA_HOME}/bin:${HADOOP_HOME}/bin:$PATH"
