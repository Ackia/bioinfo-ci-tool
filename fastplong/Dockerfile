# Fastplong multi-stage build
ARG VERSION=main
FROM ubuntu:22.04-slim AS builder
RUN apt-get update && apt-get install -y python3-pip git && rm -rf /var/lib/apt/lists/*
RUN git clone --depth 1 --branch ${VERSION} https://github.com/your-org/fastplong.git /src/fastplong
RUN pip3 wheel /src/fastplong -w /wheels

FROM ubuntu:22.04-slim
ARG VERSION
LABEL org.opencontainers.image.source="https://github.com/your-org/fastplong"
LABEL org.opencontainers.image.version="${VERSION}"
LABEL org.opencontainers.image.license="MIT"
RUN apt-get update && apt-get install -y python3-pip ca-certificates && rm -rf /var/lib/apt/lists/*
COPY --from=builder /wheels/*.whl /wheels/
RUN pip3 install /wheels/*.whl && rm -rf /wheels
ENTRYPOINT ["fastplong"]
