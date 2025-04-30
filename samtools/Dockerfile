# Samtools multi-stage build
ARG VERSION=1.17
FROM ubuntu:22.04-slim AS builder
RUN apt-get update && apt-get install -y autoconf automake build-essential git libbz2-dev liblzma-dev libncurses-dev libcurl4-gnutls-dev && rm -rf /var/lib/apt/lists/*
RUN git clone --depth 1 --branch ${VERSION} https://github.com/samtools/samtools.git /src/samtools
RUN cd /src/samtools && ./configure --prefix=/usr/local && make && make install DESTDIR=/dest

FROM ubuntu:22.04-slim
ARG VERSION
LABEL org.opencontainers.image.source="https://github.com/your-org/samtools"
LABEL org.opencontainers.image.version="${VERSION}"
LABEL org.opencontainers.image.license="MIT"
RUN apt-get update && apt-get install -y ca-certificates && rm -rf /var/lib/apt/lists/*
COPY --from=builder /dest/usr/local /usr/local
ENTRYPOINT ["samtools"]
