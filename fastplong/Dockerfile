# Fastplong prebuilt binary
FROM debian:bookworm-slim AS builder
RUN apt-get update && apt-get install -y wget && rm -rf /var/lib/apt/lists/*
RUN wget http://opengene.org/fastplong/fastplong -O /fastplong && chmod +x /fastplong

FROM debian:bookworm-slim
ARG VERSION
LABEL org.opencontainers.image.source="https://github.com/OpenGene/fastplong"
LABEL org.opencontainers.image.version="${VERSION}"
LABEL org.opencontainers.image.license="MIT"
RUN apt-get update && apt-get install -y ca-certificates wget && rm -rf /var/lib/apt/lists/*
COPY --from=builder /fastplong /usr/local/bin/fastplong
ENTRYPOINT ["fastplong"]
