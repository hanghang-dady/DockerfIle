#Dockerfile文件内容
#RocketMQ依赖Java环境，因此基于Java镜像进行构建
#修改启动参数-Xms4g -Xmx4g -Xmn2g -XX:MetaspaceSize=128m -XX:MaxMetaspaceSize=320m为-Xms256m -Xmx256m -Xmn128m -XX:MetaspaceSize=64m -XX:MaxMetaspaceSize=128m，虚拟机内存较小
#10911：消息监听端口
#10912：消息同步端口

FROM openjdk:8-alpine

#ARG user=rocketmq
#ARG group=rocketmq
#ARG uid=3000
#ARG gid=3000
  
ENV ROCKETMQ_VERSION 4.5.1

ENV ROCKETMQ_HOME /opt/rocketmq-${ROCKETMQ_VERSION}

ENV JAVA_OPT " -Duser.home=/opt"

WORKDIR ${ROCKETMQ_HOME}

RUN apk add --no-cache bash gettext nmap-ncat openssl busybox-extras curl

# Install
COPY rocketmq.zip .

RUN mkdir -p /opt/logs /opt/store \
#    && wget https://dist.apache.org/repos/dist/release/rocketmq/${ROCKETMQ_VERSION}/rocketmq-all-${ROCKETMQ_VERSION}-bin-release.zip -O rocketmq.zip \
    && unzip  rocketmq.zip \
    && mv rocketmq-all-${ROCKETMQ_VERSION}-bin-release/*  ${ROCKETMQ_HOME} \
    && rm rocketmq.zip \
    && cd ${ROCKETMQ_HOME}/bin \
    && sed -i 's#-Xms[0-9]\+[gm]#-Xms256m#' runbroker.sh \
    && sed -i 's#-Xmx[0-9]\+[gm]#-Xmx256m#' runbroker.sh \
    && sed -i 's#-Xmn[0-9]\+[gm]#-Xmn128m#' runbroker.sh \
    && chmod +x ./mqbroker

# Expose broker ports
EXPOSE 10909 10911 10912

VOLUME ["/opt/logs","/opt/store"]

WORKDIR ${ROCKETMQ_HOME}/bin
#CMD cd ${ROCKETMQ_HOME}/bin && sh mqbroker
