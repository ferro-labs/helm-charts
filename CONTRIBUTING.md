# Contributing to AI Gateway Helm Charts

Thank you for your interest in contributing to the Ferro Labs Helm charts!

## Guidelines

This repository follows the same contributing guidelines as the main AI Gateway project. Please see the [AI Gateway CONTRIBUTING.md](https://github.com/ferro-labs/ai-gateway/blob/main/CONTRIBUTING.md) for:

- Code style and conventions
- Commit message format (Conventional Commits)
- Pull request process

## Chart Development

### Prerequisites

- [Helm](https://helm.sh/docs/intro/install/) 3.10+
- [chart-testing (ct)](https://github.com/helm/chart-testing) for linting
- [KinD](https://kind.sigs.k8s.io/) for local testing

### Local Development

```bash
# Lint the chart
ct lint --config ct.yaml

# Install in a local KinD cluster
kind create cluster
helm install test charts/ai-gateway \
  --set secrets.adminApiKey=test-key \
  --set secrets.providerKeys.openai=sk-test
```

### Making Changes

1. Modify templates in `charts/ai-gateway/templates/`
2. Update `values.yaml` with sensible defaults for new fields
3. Update `values.schema.json` if adding new configuration parameters
4. Bump the chart version in `Chart.yaml`
5. Update the chart `README.md` with new parameters
6. Test with `ct lint` and `ct install`

## Questions?

Open a [GitHub Discussion](https://github.com/ferro-labs/ai-gateway/discussions) or reach out on [Discord](https://discord.gg/YYSKrgBXMz).
