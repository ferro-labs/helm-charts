# ai-gateway Helm Chart

[![Artifact Hub](https://img.shields.io/endpoint?url=https://artifacthub.io/badge/repository/ferro-labs)](https://artifacthub.io/packages/helm/ferro-labs/ai-gateway)

Helm chart for the [Ferro Labs AI Gateway](https://github.com/ferro-labs/ai-gateway) — a high-performance, multi-provider LLM proxy supporting 20+ AI providers, 6 routing strategies, and an extensible plugin pipeline.

## TL;DR

```bash
helm repo add ferro-labs https://ferro-labs.github.io/helm-charts
helm repo update
helm install ferrogw ferro-labs/ai-gateway \
  --set secrets.adminApiKey="your-admin-key" \
  --set secrets.providers.openai="sk-..." \
  --set secrets.providers.anthropic="sk-ant-..."
```

## Prerequisites

- Kubernetes 1.25+
- Helm 3.10+

## Installing the Chart

```bash
helm install ferrogw ferro-labs/ai-gateway \
  --namespace ferrogw \
  --create-namespace \
  -f my-values.yaml
```

## Uninstalling the Chart

```bash
helm uninstall ferrogw --namespace ferrogw
```

## Configuration

See [values.yaml](./values.yaml) for the full list of configurable parameters.

### Key parameters

| Parameter | Description | Default |
| --- | --- | --- |
| `replicaCount` | Number of gateway pods | `2` |
| `image.repository` | Container image repository | `ghcr.io/ferro-labs/ai-gateway` |
| `image.tag` | Image tag (defaults to chart `appVersion`) | `""` |
| `config.strategy.mode` | Routing strategy | `fallback` |
| `secrets.adminApiKey` | Secret for `/admin` endpoints | `""` |
| `secrets.providers` | Map of provider name → API key | `{}` |
| `ingress.enabled` | Enable Ingress | `false` |
| `autoscaling.enabled` | Enable HPA | `false` |
| `pdb.enabled` | Enable PodDisruptionBudget | `true` |

### Providing secrets securely

Instead of passing API keys via `--set`, use an external-secrets or sealed-secrets operator, or reference an existing Secret:

```yaml
# values.yaml
secrets:
  adminApiKey: ""        # leave empty
  providers: {}          # leave empty — keys injected by external-secrets
```

### Enabling Ingress with TLS

```yaml
ingress:
  enabled: true
  className: nginx
  annotations:
    cert-manager.io/cluster-issuer: letsencrypt-prod
  hosts:
    - host: gateway.example.com
      paths:
        - path: /
          pathType: Prefix
  tls:
    - secretName: ferrogw-tls
      hosts:
        - gateway.example.com
```

### Enabling autoscaling

```yaml
autoscaling:
  enabled: true
  minReplicas: 2
  maxReplicas: 20
  targetCPUUtilizationPercentage: 70
```

## Full documentation

→ [docs.ferrolabs.ai/guides/kubernetes](https://docs.ferrolabs.ai/guides/kubernetes)
