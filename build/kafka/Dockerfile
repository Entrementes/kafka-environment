FROM openjdk:8-jdk-slim

MAINTAINER Gunisalvo

RUN addgroup --gid 1000 entrementes && \
    adduser --uid 1200 --home /opt/kafka --ingroup entrementes --disabled-password --gecos "kafka" kafka && \
    mkdir -p /opt/kafka && \
    mkdir -p /var/lib/kafka

ADD http://ftp.unicamp.br/pub/apache/kafka/1.0.0/kafka_2.12-1.0.0.tgz /opt/kafka_2.12-1.0.0.tgz

RUN tar -xvf /opt/kafka_2.12-1.0.0.tgz  && \
    cp -R /kafka_2.12-1.0.0/* /opt/kafka/ && \
    rm -rf /kafka_2.12-1.0.0 && \
    chown -R kafka:entrementes /opt/kafka  && \
    chown kafka:entrementes /var/lib/kafka

USER kafka

WORKDIR /opt/kafka

ADD kafka.properties /opt/kafka/kafka.properties

EXPOSE 9092 9093

ENV KAFKA_ID 1

ENV KAFKA_PORT 9092

ENTRYPOINT ./bin/kafka-server-start.sh kafka.properties --override broker.id=$KAFKA_ID --override listeners=PLAINTEXT://:$KAFKA_PORT