FROM alpine:3.21

ARG TARGETARCH
ARG ATMOS_VERSION=1.207.0
ARG TOFU_VERSION=1.9.0
ARG HELM_VERSION=3.17.0
ARG HELMFILE_VERSION=0.171.0

# System dependencies
RUN apk add --no-cache bash curl jq git openssh-client

# kubectl (latest stable)
RUN curl -fsSL "https://dl.k8s.io/release/$(curl -fsSL https://dl.k8s.io/release/stable.txt)/bin/linux/${TARGETARCH}/kubectl" \
      -o /usr/local/bin/kubectl && \
    chmod +x /usr/local/bin/kubectl

# OpenTofu
RUN curl -fsSL "https://github.com/opentofu/opentofu/releases/download/v${TOFU_VERSION}/tofu_${TOFU_VERSION}_linux_${TARGETARCH}.tar.gz" \
      | tar -xz -C /usr/local/bin tofu

# Atmos
RUN curl -fsSL "https://github.com/cloudposse/atmos/releases/download/v${ATMOS_VERSION}/atmos_${ATMOS_VERSION}_linux_${TARGETARCH}" \
      -o /usr/local/bin/atmos && \
    chmod +x /usr/local/bin/atmos

# Helm
RUN curl -fsSL "https://get.helm.sh/helm-v${HELM_VERSION}-linux-${TARGETARCH}.tar.gz" \
      | tar -xz -C /usr/local/bin --strip-components=1 "linux-${TARGETARCH}/helm"

# Helmfile
RUN curl -fsSL "https://github.com/helmfile/helmfile/releases/download/v${HELMFILE_VERSION}/helmfile_${HELMFILE_VERSION}_linux_${TARGETARCH}.tar.gz" \
      | tar -xz -C /usr/local/bin helmfile

# Helm-diff plugin (required by helmfile)
ARG HELM_DIFF_VERSION=3.9.12
RUN helm plugin install https://github.com/databus23/helm-diff --version "v${HELM_DIFF_VERSION}"

WORKDIR /
