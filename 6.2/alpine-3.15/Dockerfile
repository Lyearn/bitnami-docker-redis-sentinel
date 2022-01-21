FROM alpine:3.15.0
LABEL maintainer "Lyearn <dev@lyearn.com>"

ENV HOME="/" \
    OS_ARCH="amd64" \
    OS_FLAVOUR="debian-10" \
    OS_NAME="linux"

COPY prebuildfs /
# Install required system packages and dependencies
RUN install_packages acl ca-certificates curl gzip libssl1.1 procps tar bash
RUN . /opt/bitnami/scripts/libcomponent.sh && component_unpack "redis-sentinel" "6.2.6-2" --checksum 3007df13de63e4520cf701bc72a5232c0698c740535d9a369aeac16b1b4a1496
RUN . /opt/bitnami/scripts/libcomponent.sh && component_unpack "gosu" "1.14.0-1" --checksum 16f1a317859b06ae82e816b30f98f28b4707d18fe6cc3881bff535192a7715dc

RUN chmod g+rwX /opt/bitnami
RUN ln -s /opt/bitnami/scripts/redis-sentinel/entrypoint.sh /entrypoint.sh
RUN ln -s /opt/bitnami/scripts/redis-sentinel/run.sh /run.sh

COPY rootfs /
RUN /opt/bitnami/scripts/redis-sentinel/postunpack.sh
ENV BITNAMI_APP_NAME="redis-sentinel" \
    BITNAMI_IMAGE_VERSION="6.2.6-alpine" \
    PATH="/opt/bitnami/common/bin:/opt/bitnami/redis-sentinel/bin:$PATH"

EXPOSE 26379

USER 1001
ENTRYPOINT [ "/opt/bitnami/scripts/redis-sentinel/entrypoint.sh" ]
CMD [ "/opt/bitnami/scripts/redis-sentinel/run.sh" ]
