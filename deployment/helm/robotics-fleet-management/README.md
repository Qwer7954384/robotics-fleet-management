# Robotics Fleet Management Helm Chart

AMR/AGV orchestration with A* path planning

## Installation

```bash
helm install robotics-fleet-management .
```

## Configuration

See `values.yaml` for all configuration options.

### Key Configuration

```yaml
image:
  repository: paklog/robotics-fleet-management
  tag: latest

service:
  port: 8092
  managementPort: 8081

resources:
  limits:
    cpu: 1000m
    memory: 1Gi
  requests:
    cpu: 500m
    memory: 512Mi

autoscaling:
  enabled: true
  minReplicas: 2
  maxReplicas: 10
```

### Database Configuration

MongoDB is enabled by default.

Redis is enabled for caching.

### Observability

- **Metrics**: Prometheus metrics available at `/actuator/prometheus`
- **Tracing**: OpenTelemetry traces sent to Tempo
- **Logging**: Structured logs sent to Loki

## Uninstallation

```bash
helm uninstall robotics-fleet-management
```

## Maintainers

- Paklog Team
