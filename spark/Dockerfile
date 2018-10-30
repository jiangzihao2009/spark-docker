FROM spark/base:ubuntu18.04

ENV ZOOKEEPER_VERSION=3.4.13
ENV SPARK_VERSION=2.3.2
ENV HADOOP_MAIN_VERSION=2.7
ENV HADOOP_MINOR_VERSION=2.7.7

ENV JAVA_DIR=jdk1.8.0_191

RUN mkdir -p /usr/local/zookeeper \
 && mkdir -p /usr/local/spark \
 && mkdir -p /usr/local/hadoop

COPY ./zookeeper-${ZOOKEEPER_VERSION}.tar.gz /tmp
COPY ./hadoop-{HADOOP_MINOR_VERSION}.tar.gz /tmp
COPY ./spark-${SPARK_VERSION}-bin-hadoop${HADOOP_MAIN_VERSION}.tgz /tmp

# setup zookeeper & hadoop & spark
RUN tar -zxvf /tmp/zookeeper-${ZOOKEEPER_VERSION}.tar.gz -C /tmp \
 && cp -rf /tmp/zookeeper-${ZOOKEEPER_VERSION}/* /usr/local/zookeeper \
 && rm -rf /tmp/zookeeper-${ZOOKEEPER_VERSION}.tar.gz && rm -rf /tmp/zookeeper-${ZOOKEEPER_VERSION}

# set the enviroment variables
 ENV ZOOKEEPER_HOME "/usr/local/zookeeper"
 ENV PATH "${ZOOKEEPER_HOME}/bin:$PATH"

