# BWA multi-stage build
ARG VERSION=0.7.17
FROM ubuntu:22.04-slim AS builder
RUN apt-get update && apt-get install -y build-essential git zlib1g-dev && rm -rf /var/lib/apt/lists/*
RUN git clone --depth 1 --branch v${VERSION} https://github.com/lh3/bwa.git /src/bwa
RUN cd /src/bwa && make

FROM ubuntu:22.04-slim
ARG VERSION
LABEL org.opencontainers.image.source="https://github.com/your-org/bwa"
LABEL org.opencontainers.image.version="${VERSION}"
LABEL org.opencontainers.image.license="MIT"
RUN apt-get update && apt-get install -y ca-certificates && rm -rf /var/lib/apt/lists/*
COPY --from=builder /src/bwa/bwa /usr/local/bin/
ENTRYPOINT ["bwa"]
