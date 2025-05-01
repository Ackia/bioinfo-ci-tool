# Minimap2 multi-stage build
ARG VERSION=2.24
FROM debian:bookworm-slim AS builder
ARG VERSION
RUN apt-get update && apt-get install -y build-essential git zlib1g-dev && rm -rf /var/lib/apt/lists/*
RUN git clone --depth 1 --branch v${VERSION} https://github.com/lh3/minimap2.git /src/minimap2
RUN cd /src/minimap2 && make -j$(nproc)

FROM debian:bookworm-slim
ARG VERSION
LABEL org.opencontainers.image.source="https://github.com/lh3/minimap2"
LABEL org.opencontainers.image.version="${VERSION}"
LABEL org.opencontainers.image.license="MIT"
RUN apt-get update && apt-get install -y ca-certificates && rm -rf /var/lib/apt/lists/*
COPY --from=builder /src/minimap2/minimap2 /usr/local/bin/
ENTRYPOINT ["minimap2"]
