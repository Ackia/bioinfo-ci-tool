# Minimap2 multi-stage build
ARG VERSION=2.29
FROM debian:bookworm-slim AS builder
ARG VERSION
RUN apt-get update && apt-get install -y wget git build-essential curl zlib1g-dev && rm -rf /var/lib/apt/lists/*
RUN mkdir -p /src
RUN curl -L https://github.com/lh3/minimap2/releases/download/v${VERSION}/minimap2-${VERSION}_x64-linux.tar.bz2 | tar jxf -
RUN cp minimap2-${VERSION}_x64-linux/{minimap2,k8,paftools.js} /src/
WORKDIR /src
ENV PATH="/src:$PATH"

FROM debian:bookworm-slim
ARG VERSION
LABEL org.opencontainers.image.source="https://github.com/lh3/minimap2"
LABEL org.opencontainers.image.version="${VERSION}"
LABEL org.opencontainers.image.license="MIT"
RUN apt-get update && apt-get install -y ca-certificates zlib1g && rm -rf /var/lib/apt/lists/*
COPY --from=builder /src/ /usr/local/bin/
ENTRYPOINT ["minimap2"]
