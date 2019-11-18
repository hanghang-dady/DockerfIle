#Dockerfile文件内容
#RocketMQ Java环境
#修改启动参数-Xms4g -Xmx4g -Xmn2g -XX:MetaspaceSize=128m -XX:MaxMetaspaceSize=320m为-Xms256m -Xmx256m -Xmn128m -XX:MetaspaceSize=64m -XX:MaxMetaspaceSize=128m，虚拟机内存较小
#9876：消息监听端口

FROM openjdk:8-alpine

#ARG user=rocketmq
#ARG group=rocketmq
#ARG uid=3000
#ARG gid=3000
  
ENV ROCKETMQ_VERSION 4.5.1

ENV ROCKETMQ_HOME /opt/rocketmq-${ROCKETMQ_VERSION}
ENV JAVA_OPT " -Duser.home=/opt"

WORKDIR ${ROCKETMQ_HOME}

RUN apk add --no-cache bash gettext nmap-ncat openssl busybox-extras

# Install
COPY rocketmq.zip .

RUN mkdir -p /opt/logs /opt/store \
#    && wget https://dist.apache.org/repos/dist/release/rocketmq/${ROCKETMQ_VERSION}/rocketmq-all-${ROCKETMQ_VERSION}-bin-release.zipi -O rocketmq.zip  \ 
    && unzip  rocketmq.zip \
    && mv rocketmq-all-${ROCKETMQ_VERSION}-bin-release/* ${ROCKETMQ_HOME} \
    && rm rocketmq.zip \
    && cd ${ROCKETMQ_HOME}/bin \
    && sed -i 's#-Xms[0-9]\+[gm]#-Xms256m#' runserver.sh \
    && sed -i 's#-Xmx[0-9]\+[gm]#-Xmx256m#' runserver.sh \
    && sed -i 's#-Xmn[0-9]\+[gm]#-Xmn128m#' runserver.sh \
    && sed -i 's#-XX:MetaspaceSize=[0-9]\+[gm]#-XX:MetaspaceSize=64m#' runserver.sh \
    && sed -i 's#-XX:MaxMetaspaceSize=[0-9]\+[gm]#-XX:MaxMetaspaceSize=128m#' runserver.sh \
    && chmod +x ./mqnamesrv

EXPOSE 9876

VOLUME ["/opt/logs","/opt/store"]

CMD cd ${ROCKETMQ_HOME}/bin && sh mqnamesrv
