# Bioinformatics Docker Images

This repository contains Dockerfiles and GitHub Actions workflows to build and publish minimal Docker images for:

- **minimap2**: Versatile sequence alignment tool
- **bwa**: Burrows-Wheeler aligner
- **samtools**: SAM/BAM toolkit
- **fastplong**: Long-read processing tool

Key features:

- Multi-stage builds on `ubuntu:22.04-slim`
- Parameterized `VERSION` build-arg
- Minimal runtime images with only necessary binaries and CA certificates
- CI/CD pipelines via GitHub Actions (push, manual dispatch, repository_dispatch)
- Multi-architecture builds (`amd64` and `arm64`)
- Published to GitHub Container Registry (`ghcr.io/your-org/<tool>`)

## Usage

Build locally:

```bash
docker build --build-arg VERSION=2.24 -t minimap2:2.24 ./minimap2
```

Run:

```bash
docker run --rm minimap2:2.24 --help
```

For details on CI triggers and modifications, see the workflows in `.github/workflows/`.
