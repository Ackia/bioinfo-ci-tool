# Samtools multi-stage build
ARG VERSION=1.21
FROM debian:bookworm-slim AS builder
ARG VERSION
RUN apt-get update && apt-get install -y wget bzip2 build-essential libncurses5-dev zlib1g-dev libbz2-dev liblzma-dev && rm -rf /var/lib/apt/lists/*
RUN mkdir -p /src \
    && wget https://github.com/samtools/samtools/releases/download/${VERSION}/samtools-${VERSION}.tar.bz2 -O /src/samtools-${VERSION}.tar.bz2 \
    && tar xj -f /src/samtools-${VERSION}.tar.bz2 -C /src
WORKDIR /src/samtools-${VERSION}
RUN ./configure --prefix=/usr/local && make -j$(nproc) && make install DESTDIR=/dest

FROM debian:bookworm-slim
ARG VERSION
LABEL org.opencontainers.image.source="https://github.com/samtools/samtools"
LABEL org.opencontainers.image.version="${VERSION}"
LABEL org.opencontainers.image.license="MIT"
RUN apt-get update && apt-get install -y ca-certificates libncursesw6 zlib1g libbz2-1.0 liblzma5 libcurl4 && rm -rf /var/lib/apt/lists/*
COPY --from=builder /dest/usr/local /usr/local
ENTRYPOINT ["samtools"]
