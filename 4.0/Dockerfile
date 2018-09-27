FROM ubuntu:18.04 as builder

ARG REDIS_VERSION=4.0.11

WORKDIR /root

RUN apt-get update && \
    DEBIAN_FRONTEND=noninteractive apt-get install build-essential wget curl -y -o Dpkg::Options::='--force-confdef' -o Dpkg::Options::='--force-confold' && \
    wget https://github.com/antirez/redis/archive/${REDIS_VERSION}.tar.gz && \
    tar zxf ${REDIS_VERSION}.tar.gz && \
    cd redis-${REDIS_VERSION}/src && \
    make noopt

FROM ubuntu:18.04
RUN apt-get update && \
    DEBIAN_FRONTEND=noninteractive apt-get install gdb gdbserver cgdb -y -o Dpkg::Options::='--force-confdef' -o Dpkg::Options::='--force-confold' && \
    rm /etc/sysctl.d/10-ptrace.conf && \
    sysctl -p

COPY --from=builder /root /root
