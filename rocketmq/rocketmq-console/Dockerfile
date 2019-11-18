FROM openjdk:8-alpine

VOLUME /tmp

ADD rocketmq-console-1.0.1.jar rocketmq-console.jar

RUN sh -c 'touch /rocketmq-console.jar'

ENV JAVA_OPTS ""

ENV NAMESRV_ADDR ""

EXPOSE 8080

ENTRYPOINT [ "sh", "-c", "java $JAVA_OPTS -jar /rocketmq-console.jar" ]
