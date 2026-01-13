FROM ubuntu:16.04

ENV GOPATH=/go
ENV PATH="/go/bin:/usr/local/go/bin:${PATH}"

ARG GO_VERSION=1.24.0
ARG GO_DOWNLOAD_URL=https://go.dev/dl/go${GO_VERSION}.linux-amd64.tar.gz

ARG GCC_ARM_VERSION=gcc-linaro-5.3.1-2016.05-x86_64_arm-linux-gnueabi
# ARG GCC_ARM_URL=https://releases.linaro.org/components/toolchain/binaries/5.3-2016.05/arm-linux-gnueabi/${GCC_ARM_VERSION}.tar.xz

ARG GCC_AARCH64_VERSION=gcc-linaro-7.4.1-2019.02-x86_64_aarch64-linux-gnu
# ARG GCC_AARCH64_URL=https://releases.linaro.org/components/toolchain/binaries/7.4-2019.02/aarch64-linux-gnu/${GCC_AARCH64_VERSION}.tar.xz

WORKDIR /app

RUN sed -i 's|http://.*.ubuntu.com|http://mirrors.aliyun.com|g' /etc/apt/sources.list && \
    apt-get update && apt-get install -y --no-install-recommends \
    gcc wget curl ca-certificates git build-essential xz-utils && \
    rm -rf /var/lib/apt/lists/*

# RUN curl -L ${GCC_ARM_URL} -o /opt/${GCC_ARM_VERSION}.tar.xz && \
#     tar -xJf /opt/${GCC_ARM_VERSION}.tar.xz -C /opt && \
#     rm -f /opt/${GCC_ARM_VERSION}.tar.xz

# RUN curl -L ${GCC_AARCH64_URL} -o /opt/${GCC_AARCH64_VERSION}.tar.xz && \
#     tar -xJf /opt/${GCC_AARCH64_VERSION}.tar.xz -C /opt && \
#     rm -f /opt/${GCC_AARCH64_VERSION}.tar.xz

COPY ./gcc-linaro-5.3.1-2016.05-x86_64_arm-linux-gnueabi.tar.gz /opt/
COPY ./gcc-linaro-7.4.1-2019.02-x86_64_aarch64-linux-gnu.tar.gz /opt/

RUN tar -xzvf /opt/gcc-linaro-5.3.1-2016.05-x86_64_arm-linux-gnueabi.tar.gz -C /opt && \
    tar -xzvf /opt/gcc-linaro-7.4.1-2019.02-x86_64_aarch64-linux-gnu.tar.gz -C /opt && \
    rm -f /opt/*.tar.gz

RUN curl -fsSL https://go.dev/dl/go${GO_VERSION}.linux-amd64.tar.gz -o /tmp/go.tar.gz && \
    tar -C /usr/local -xzf /tmp/go.tar.gz && \
    rm -f /tmp/go.tar.gz
