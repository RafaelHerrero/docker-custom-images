FROM hashicorp/vault:1.18

# Install kubectl with multi-platform support
ARG TARGETARCH
RUN apk add --no-cache curl && \
    curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/${TARGETARCH}/kubectl" && \
    install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl && \
    rm kubectl

# Install jq for JSON processing
RUN apk add --no-cache jq

WORKDIR /
