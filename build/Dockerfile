FROM java:alpine
MAINTAINER zhoutaoo "zhoutaoo@foxmail.com"

# set environment
ENV BASE_DIR="/home/sentinel" \
    SERVER_PORT="8021" \
    DASHBOARD_SERVER="localhost:8021" \
    PROJECT_NAME="sentinel-dashboard" \
    JAVA_OPTS="" \
    TIME_ZONE="Asia/Shanghai"

ARG SENTINEL_DASHBOARD_VERSION=1.6.3

WORKDIR /$BASE_DIR

RUN set -x \
    && apk --no-cache add ca-certificates wget \
    && update-ca-certificates \
    && wget https://github.com/alibaba/Sentinel/releases/download/${SENTINEL_DASHBOARD_VERSION}/sentinel-dashboard-${SENTINEL_DASHBOARD_VERSION}.jar -P $BASE_DIR \
    && ln -snf /usr/share/zoneinfo/$TIME_ZONE /etc/localtime && echo '$TIME_ZONE' > /etc/timezone

ADD bin/docker-entrypoint.sh bin/docker-entrypoint.sh

# set startup log dir
RUN mkdir -p logs \
	&& cd logs \
	&& touch start.out \
	&& ln -sf /dev/stdout start.out \
	&& ln -sf /dev/stderr start.out
RUN chmod +x bin/docker-entrypoint.sh

EXPOSE 8021
ENTRYPOINT ["bin/docker-entrypoint.sh"]
