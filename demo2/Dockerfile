FROM openjdk:8u191-jdk-alpine3.8
MAINTAINER foxiswho@gmail.com

ARG version
ARG ip
ARG port

# sentinel version
ENV SENTINEL_VERSION ${version:-1.4.1}
#host
ENV IP ${ip:-localhost}
#ip
ENV PORT ${port:-8080}


# sentinel home
ENV SENTINEL_HOME  /opt/
ENV SENTINEL_LOGS  /opt/logs

#tme zone
RUN rm -rf /etc/localtime \
&& ln -s /usr/share/zoneinfo/Asia/Shanghai /etc/localtime

# create logs
RUN mkdir -p ${SENTINEL_LOGS}

# test file
COPY sentinel-dashboard.jar ${SENTINEL_HOME}

# add scripts
#COPY scripts/* /usr/local/bin/
RUN chmod +x /usr/local/bin/docker-entrypoint.sh \
&& ln -s /usr/local/bin/docker-entrypoint.sh /docker-entrypoint.sh

#
RUN chmod -R +x ${SENTINEL_HOME}/*jar

VOLUME ${SENTINEL_LOGS}

WORKDIR  ${SENTINEL_HOME}

EXPOSE ${PORT}

CMD java ${JAVA_OPTS} -jar sentinel-dashboard.jar