# Ferro Labs Helm Charts

[![Artifact Hub](https://img.shields.io/endpoint?url=https://artifacthub.io/badge/repository/ferro-labs)](https://artifacthub.io/packages/search?org=ferro-labs)

Official Helm charts for [Ferro Labs](https://ferrolabs.ai) — starting with the AI Gateway.

## Charts

| Chart | Description | Version |
| --- | --- | --- |
| [ai-gateway](./charts/ai-gateway/) | High-performance multi-provider LLM proxy | 1.0.4 |

## Quick install

```bash
helm repo add ferro-labs https://ferro-labs.github.io/helm-charts
helm repo update

helm install ferrogw ferro-labs/ai-gateway \
  --version 1.0.4 \
  --set secrets.adminApiKey="your-admin-key" \
  --set secrets.providers.openai="sk-..." \
  --set secrets.providers.anthropic="sk-ant-..."
```

## Documentation

Full deployment guide: [docs.ferrolabs.ai/guides/kubernetes](https://docs.ferrolabs.ai/guides/kubernetes)

## Contributing

Charts are linted and installed on every PR via [chart-testing](https://github.com/helm/chart-testing).
See [.github/workflows/lint-test.yml](.github/workflows/lint-test.yml) for the CI setup.
