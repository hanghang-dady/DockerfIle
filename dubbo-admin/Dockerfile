FROM openjdk:8-jdk
RUN mkdir /source \
      && wget https://github.com/apache/incubator-dubbo-admin/archive/0.2.0.zip \
      && unzip 0.2.0.zip -d /source
WORKDIR /source/incubator-dubbo-admin-0.2.0
RUN ./mvn clean package -Dmaven.test.skip=true

FROM openjdk:8-jdk
LABEL maintainer="renpengfei@163.com"
COPY --from=0 /source/incubator-dubbo-admin-0.2.0/dubbo-admin-distribution/target/dubbo-admin-0.1.tar /app.jar
ENTRYPOINT ["java","-XX:+UnlockExperimentalVMOptions","-XX:+UseCGroupMemoryLimitForHeap","-Djava.security.egd=file:/dev/./urandom","-jar","/app.jar"]
