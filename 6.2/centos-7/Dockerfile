FROM centos:7
LABEL maintainer "Bitnami <containers@bitnami.com>"

ENV HOME="/" \
    OS_ARCH="x86_64" \
    OS_FLAVOUR="centos-7" \
    OS_NAME="linux" \
    PATH="/opt/bitnami/redis-sentinel/bin:/opt/bitnami/common/bin:$PATH"

COPY prebuildfs /

RUN yum install -y epel-release

# Install required system packages and dependencies
RUN yum install -y acl ca-certificates curl gzip glibc openssl procps tar
RUN . /opt/bitnami/scripts/libcomponent.sh && component_unpack "redis-sentinel" "6.2.7-2" --checksum 0c8230908565b3003a59d83fd9c286281450948ef1302d9dee913678ccedbf5e
RUN . /opt/bitnami/scripts/libcomponent.sh && component_unpack "gosu" "1.14.0-1" --checksum 5d374042b9320f3c931294d854835ffe602b499b2d71a4274769e12e6ba37eb7
RUN yum update -y && yum upgrade -y && \
    yum clean all && rm -fR /var/cache/yum
RUN chmod g+rwX /opt/bitnami

COPY rootfs /
RUN /opt/bitnami/scripts/redis-sentinel/postunpack.sh
ENV BITNAMI_APP_NAME="redis-sentinel" \
    BITNAMI_IMAGE_VERSION="6.2.6-debian-10-r103"

EXPOSE 26379

USER 1001
ENTRYPOINT [ "/opt/bitnami/scripts/redis-sentinel/entrypoint.sh" ]
CMD [ "/opt/bitnami/scripts/redis-sentinel/run.sh" ]
