FROM openjdk:8-jdk-slim

MAINTAINER Gunisalvo

RUN addgroup --gid 1000 entrementes && \
    adduser --uid 1100 --home /opt/zookeeper --ingroup entrementes --disabled-password --gecos "zookeeper" zookeeper && \
    mkdir -p /opt/zookeeper && \
    mkdir -p /var/lib/zookeeper

ADD http://ftp.unicamp.br/pub/apache/zookeeper/zookeeper-3.4.11/zookeeper-3.4.11.tar.gz /opt/zookeeper-3.4.11.tar.gz

RUN tar -xvf /opt/zookeeper-3.4.11.tar.gz  && \
    cp -R /zookeeper-3.4.11/* /opt/zookeeper/ && \
    rm -rf /zookeeper-3.4.11 && \
    chown -R zookeeper:entrementes /opt/zookeeper  && \
    chown zookeeper:entrementes /var/lib/zookeeper

USER zookeeper

WORKDIR /opt/zookeeper

ADD zoo.cfg /opt/zookeeper/conf/zoo.cfg

EXPOSE 2181 2888 3888

ENTRYPOINT /opt/zookeeper/bin/zkServer.sh start-foreground
