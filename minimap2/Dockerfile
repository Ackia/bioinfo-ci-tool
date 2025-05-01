# Minimap2 multi-stage build
ARG VERSION=2.24
FROM debian:bookworm-slim AS builder
ARG VERSION
RUN apt-get update && apt-get install -y wget build-essential zlib1g-dev && rm -rf /var/lib/apt/lists/*
RUN mkdir -p /src \
    && wget https://github.com/lh3/minimap2/releases/download/v${VERSION}/minimap2-${VERSION}.tar.bz2 -O /src/minimap2-${VERSION}.tar.bz2 \
    && tar xjf /src/minimap2-${VERSION}.tar.bz2 -C /src
WORKDIR /src/minimap2-${VERSION}
RUN make

FROM debian:bookworm-slim
ARG VERSION
LABEL org.opencontainers.image.source="https://github.com/lh3/minimap2"
LABEL org.opencontainers.image.version="${VERSION}"
LABEL org.opencontainers.image.license="MIT"
RUN apt-get update && apt-get install -y ca-certificates zlib1g && rm -rf /var/lib/apt/lists/*
COPY --from=builder /src/minimap2-${VERSION}/minimap2 /usr/local/bin/
ENTRYPOINT ["minimap2"]
