# Docker Custom Images

Custom Docker images for various projects.

## Available Images

### vault-kubectl-jq

Consolidated image with Vault, kubectl, and jq for Kubernetes init jobs.

**Pull:**
```bash
docker pull ghcr.io/rherrero/dcaf-k8s/vault-kubectl-jq:latest
```

**Contains:**
- hashicorp/vault:1.18
- kubectl (latest stable)
- jq

**Usage:**
```yaml
containers:
  - name: init
    image: ghcr.io/rherrero/dcaf-k8s/vault-kubectl-jq:v1.0.0
```

## Building & Pushing

Images are automatically built and pushed to GitHub Container Registry when a version tag is pushed:

```bash
git tag v1.0.0
git push --tags
```

This triggers the GitHub workflow which builds and pushes:
- `ghcr.io/rherrero/dcaf-k8s/vault-kubectl-jq:v1.0.0`
- `ghcr.io/rherrero/dcaf-k8s/vault-kubectl-jq:latest`

## Adding New Images

1. Create a new folder under `src/` (e.g., `src/new-image/`)
2. Add a `Dockerfile` inside
3. Add a new job in `.github/workflows/build.yaml` following the existing pattern
