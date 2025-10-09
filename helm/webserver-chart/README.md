# Webserver Helm Chart

A simple webserver Helm chart for OpenShift using Nginx.

## Features

- Nginx webserver deployment
- OpenShift Route for external access
- Security contexts configured for OpenShift
- Resource limits and requests
- Liveness and readiness probes

## Installation

```bash
helm install my-webserver ./webserver-chart
```

## Uninstallation

```bash
helm uninstall my-webserver
```

## Configuration

The following table lists the configurable parameters:

| Parameter | Description | Default |
|-----------|-------------|---------|
| `replicaCount` | Number of replicas | `1` |
| `image.repository` | Image repository | `nginx` |
| `image.tag` | Image tag | `1.25` |
| `service.port` | Service port | `8080` |
| `resources.limits.cpu` | CPU limit | `200m` |
| `resources.limits.memory` | Memory limit | `256Mi` |

## Example Custom Values

```bash
helm install my-webserver ./webserver-chart \
  --set replicaCount=2 \
  --set image.tag=1.26
```

Or using a custom values file:

```bash
helm install my-webserver ./webserver-chart -f custom-values.yaml
```

