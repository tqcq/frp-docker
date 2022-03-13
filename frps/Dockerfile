FROM alpine:3 AS temp

ENV FRP_VERSION="0.40.0"
ARG ARCH="amd64"
ARG FRP_URL="https://github.com/fatedier/frp/releases/download/v${FRP_VERSION}/frp_${FRP_VERSION}_linux_${ARCH}.tar.gz"

RUN mkdir -v /tmp/frp && \
    cd /tmp/frp/ && \
    wget --no-verbose ${FRP_URL} -P /tmp/frp && \
    tar xvf frp_${FRP_VERSION}_linux_${ARCH}.tar.gz && \
    chmod a+x frp_${FRP_VERSION}_linux_${ARCH}/frps && \
    cp frp_${FRP_VERSION}_linux_${ARCH}/frps /usr/bin

FROM alpine:3

COPY --from=temp /usr/bin/frps /usr/bin/frps
WORKDIR /frp

ENTRYPOINT ["/usr/bin/frps", "-c", "/frp/frps.ini"]
