FROM docker.io/bitnami/minideb:buster
LABEL maintainer "Bitnami <containers@bitnami.com>"

ENV HOME="/" \
    OS_ARCH="amd64" \
    OS_FLAVOUR="debian-10" \
    OS_NAME="linux"

COPY prebuildfs /
# Install required system packages and dependencies
RUN install_packages acl ca-certificates curl gzip libaio1 libc6 procps rsync tar zlib1g
RUN . /opt/bitnami/scripts/libcomponent.sh && component_unpack "wait-for-port" "1.0.0-3" --checksum 7521d9a4f9e4e182bf32977e234026caa7b03759799868335bccb1edd8f8fd12
RUN . /opt/bitnami/scripts/libcomponent.sh && component_unpack "java" "11.0.12-0" --checksum 14c1274e93b1135d4d1b82ad7985fc2fa7f5d0689b6da18e0c94da37407cd4ea
RUN . /opt/bitnami/scripts/libcomponent.sh && component_unpack "keycloak" "15.0.2-0" --checksum 397ddf03ec7267a291448fe82d7ae1285cc3c06112e0045bf1c9b4a1df417c22
RUN . /opt/bitnami/scripts/libcomponent.sh && component_unpack "gosu" "1.14.0-0" --checksum 3e6fc37ca073b10a73a804d39c2f0c028947a1a596382a4f8ebe43dfbaa3a25e
RUN chmod g+rwX /opt/bitnami

COPY rootfs /
RUN /opt/bitnami/scripts/keycloak/postunpack.sh
ENV BITNAMI_APP_NAME="keycloak" \
    BITNAMI_IMAGE_VERSION="15.0.2-debian-10-r10" \
    PATH="/opt/bitnami/common/bin:/opt/bitnami/java/bin:/opt/bitnami/keycloak/bin:$PATH"

USER 1001
ENTRYPOINT [ "/opt/bitnami/scripts/keycloak/entrypoint.sh" ]
CMD [ "/opt/bitnami/scripts/keycloak/run.sh" ]
