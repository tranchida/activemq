FROM eclipse-temurin:17-jre-alpine

ENV ACTIVEMQ_VERSION 5.18.3
ENV ACTIVEMQ apache-activemq-$ACTIVEMQ_VERSION
ENV ACTIVEMQ_HOME /opt/activemq

RUN apk add --update curl && \
    rm -rf /var/cache/apk/* && \
    mkdir -p /opt && \
    curl -s -S https://archive.apache.org/dist/activemq/$ACTIVEMQ_VERSION/$ACTIVEMQ-bin.tar.gz | tar -xvz -C /opt && \
    mv /opt/$ACTIVEMQ $ACTIVEMQ_HOME && \
    addgroup -S activemq --gid 1001 && \
    adduser -S -H -G activemq -h $ACTIVEMQ_HOME activemq --uid 1000 && \
    chown -R activemq:activemq $ACTIVEMQ_HOME && \
    chown -h activemq:activemq $ACTIVEMQ_HOME && \
    chmod 400 ${ACTIVEMQ_HOME}/conf/jmx.password

EXPOSE 1883 5672 8161 61613 61614 61616

USER activemq
WORKDIR ${ACTIVEMQ_HOME}

CMD [ "bin/activemq", "console" ]
