# Database Helm Chart

A simple PostgreSQL database Helm chart for OpenShift.

## Features

- PostgreSQL database deployment
- Persistent storage support
- Secret management for credentials
- Security contexts configured for OpenShift
- Resource limits and requests
- Liveness and readiness probes

## Installation

```bash
helm install my-database ./database-chart
```

## Uninstallation

```bash
helm uninstall my-database
```

**Note:** Uninstalling will not delete the PersistentVolumeClaim by default. To delete it:

```bash
kubectl delete pvc -l app.kubernetes.io/instance=my-database
```

## Configuration

The following table lists the configurable parameters:

| Parameter | Description | Default |
|-----------|-------------|---------|
| `replicaCount` | Number of replicas | `1` |
| `image.repository` | Image repository | `postgres` |
| `image.tag` | Image tag | `15` |
| `database.name` | Database name | `mydb` |
| `database.user` | Database user | `dbuser` |
| `database.password` | Database password | `changeme123` |
| `persistence.enabled` | Enable persistence | `true` |
| `persistence.size` | Storage size | `1Gi` |
| `resources.limits.cpu` | CPU limit | `500m` |
| `resources.limits.memory` | Memory limit | `512Mi` |

## Example Custom Values

```bash
helm install my-database ./database-chart \
  --set database.password=mysecurepassword \
  --set persistence.size=5Gi
```

Or using a custom values file:

```bash
helm install my-database ./database-chart -f custom-values.yaml
```

## Connecting to the Database

From within the cluster:

```bash
# Get the service name
kubectl get svc -l app.kubernetes.io/name=database

# Connect using psql
PGPASSWORD=changeme123 psql -h <service-name> -U dbuser -d mydb
```

