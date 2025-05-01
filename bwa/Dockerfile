# BWA multi-stage build
ARG VERSION=0.7.17
FROM debian:bookworm-slim AS builder
ARG VERSION
RUN apt-get update && apt-get install -y wget build-essential zlib1g-dev && rm -rf /var/lib/apt/lists/*
RUN mkdir -p /src \
    && wget https://github.com/lh3/bwa/releases/download/v${VERSION}/bwa-${VERSION}.tar.bz2 -O /src/bwa-${VERSION}.tar.bz2 \
    && tar xjf /src/bwa-${VERSION}.tar.bz2 -C /src
WORKDIR /src/bwa-${VERSION}
RUN make

FROM debian:bookworm-slim
ARG VERSION
LABEL org.opencontainers.image.source="https://github.com/lh3/bwa"
LABEL org.opencontainers.image.version="${VERSION}"
LABEL org.opencontainers.image.license="MIT"
RUN apt-get update && apt-get install -y ca-certificates zlib1g && rm -rf /var/lib/apt/lists/*
COPY --from=builder /src/bwa-${VERSION}/bwa /usr/local/bin/
ENTRYPOINT ["bwa"]
