FROM ubuntu:18.04

ENV JAVA_VERSION=8u191
ENV CONDA_VERSION=5.3.0
ENV SCALA_VERSION=2.12.7 
ENV JAVA_DIR=jdk1.8.0_191
ENV ZOOKEEPER_VERSION=3.4.13

RUN mkdir -p /usr/local/java \ && mkdir -p /usr/local/scala

COPY ./jdk-${JAVA_VERSION}-linux-x64.tar.gz /tmp
COPY ./Anaconda3-${CONDA_VERSION}-Linux-x86_64.sh /tmp
COPY ./scala-${SCALA_VERSION}.tgz /tmp
COPY ./.vimrc /root

RUN apt-get update \
 && apt-get install -y \
            git \
            wget \
            cmake \
            build-essential \
            curl \
            unzip \
            flex \
            bison \
            vim \
            golang-go \
            maven \
            net-tools \
            inetutils-ping \
            tree \
            netcat \
            rsync \
            openssh-server

# setup anaconda & java & scala
RUN apt-get clean \
 && /bin/bash /tmp/Anaconda3-${CONDA_VERSION}-Linux-x86_64.sh -b -p /usr/local/anaconda \
 && rm /tmp/Anaconda3-${CONDA_VERSION}-Linux-x86_64.sh \
 && /usr/local/anaconda/bin/conda install -y libgcc \
 && /usr/local/anaconda/bin/pip install --upgrade pip \
 && tar -zxvf /tmp/jdk-${JAVA_VERSION}-linux-x64.tar.gz -C /tmp \
 && cp -rf /tmp/${JAVA_DIR}/* /usr/local/java \
 && rm /tmp/jdk-${JAVA_VERSION}-linux-x64.tar.gz && rm -rf /tmp/${JAVA_DIR} \
 && tar -zxvf /tmp/scala-${SCALA_VERSION}.tgz -C /tmp \
 && cp -rf /tmp/scala-${SCALA_VERSION}/* /usr/local/scala \
 && rm /tmp/scala-${SCALA_VERSION}.tgz && rm -rf /tmp/scala-${SCALA_VERSION}

# set the enviroment variables
 ENV JAVA_HOME "/usr/local/java"
 ENV CLASS_PATH "${JAVA_HOME}/jre/lib:${JAVA_HOME}/lib"
 ENV PATH "${JAVA_HOME}/bin:/usr/local/scala/bin:/usr/local/anaconda/bin:/usr/local/zookeeper/bin:$PATH"

