<h1 style="background-color:yellow ; color: black">Dashboard setup instructions (delete this panel after setup)</h1>

This dashboard requires:

## Metrics

Send OpenTelemetry metrics to the OTLP endpoint of a Prometheus database.

### Prometheus

Send OpenTelemetry metrics to the Prometheus OTLP Endpoint and configure the parameters `keep_identifying_resource_attributes` and `promote_resource_attributes` on the OTLP endpoint. 

Example Prometheus OTLP Endpoint configuration snippet:

```yml
otlp:
  keep_identifying_resource_attributes: true
  promote_resource_attributes:
    # REQUIRED FOR THIS DASHBOARD
    - service.instance.id
    - service.name
    - service.namespace
    - deployment.environment.name
    # RECOMMENDED FOR OTEL METRICS IN GENERAL
    - service.version
    - cloud.availability_zone
    - cloud.region
    - container.name
    - deployment.environment
    - k8s.cluster.name
    - k8s.container.name
    - k8s.cronjob.name
    - k8s.daemonset.name
    - k8s.deployment.name
    - k8s.job.name
    - k8s.namespace.name
    - k8s.pod.name
    - k8s.replicaset.name
    - k8s.statefulset.name
```

Learn more in Prometheus [configuration reference](https://prometheus.io/docs/prometheus/latest/configuration/configuration/) and [OpenTelemetry guide](https://prometheus.io/docs/guides/opentelemetry/).

### Mimir OTLP Endpoint configuration

Send OpenTelemetry metrics to the Mimir OTLP Endpoint and configure the parameters `otel_keep_identifying_resource_attributes` and `promote_otel_resource_attributes` on the OTLP endpoint. 

Example Mimir OTLP Endpoint configuration snippet:

```yml
# (experimental) Whether to keep identifying OTel resource attributes in the
# target_info metric on top of converting to job and instance labels.
# CLI flag: -distributor.otel-keep-identifying-resource-attributes
otel_keep_identifying_resource_attributes: true
# (experimental) Optionally specify OTel resource attributes to promote to
# labels.
# CLI flag: -distributor.otel-promote-resource-attributes
promote_otel_resource_attributes: "service.instance.id, service.name, service.namespace, service.version, cloud.availability_zone, cloud.region, container.name, deployment.environment, deployment.environment.name, k8s.cluster.name, k8s.container.name, k8s.cronjob.name, k8s.daemonset.name, k8s.deployment.name, k8s.job.name, k8s.namespace.name, k8s.pod.name, k8s.replicaset.name, k8s.statefulset.name"
```

Learn more in Mimir [configuration parameters](https://github.com/grafana/mimir/blob/main/docs/sources/mimir/configure/configuration-parameters/index.md).

### Grafana Cloud Metrics

Send OpenTelemetry metrics to the Grafana Cloud OTLP Endpoint as documented in [Grafana Cloud / Send OTLP data](https://grafana.com/docs/grafana-cloud/send-data/otlp/send-data-otlp/) and open a support ticket to activate `otel_keep_identifying_resource_attributes`.

Note that the Grafana Cloud OTLP Endpoint is configured by default to promote the following resource attributes, this list can be modified through a support ticket:

```
# REQUIRED FOR THIS DASHBOARD
- service.instance.id
- service.name
- service.namespace
- deployment.environment.name
# RECOMMENDED FOR OTEL METRICS IN GENERAL
- service.version
- cloud.availability_zone
- cloud.region
- container.name
- deployment.environment
- k8s.cluster.name
- k8s.container.name
- k8s.cronjob.name
- k8s.daemonset.name
- k8s.deployment.name
- k8s.job.name
- k8s.namespace.name
- k8s.pod.name
- k8s.replicaset.name
- k8s.statefulset.name
```

## Logs

### Grafana Cloud Logs

Send OpenTelemetry logs to the Grafana Cloud OTLP Endpoint as documented in [Grafana Cloud / Send OTLP data](https://grafana.com/docs/grafana-cloud/send-data/otlp/send-data-otlp/) and open a support ticket to activate `otel_keep_identifying_resource_attributes`.

### Loki

Send OpenTelemetry logs to the Loki OTLP Endpoint as documented in [Loki / Send data / OpenTelemetry](https://grafana.com/docs/loki/latest/send-data/otel/).

## Traces

### Grafana Cloud Traces

Send OpenTelemetry traces to the Grafana Cloud OTLP Endpoint as documented in [Grafana Cloud / Send OTLP data](https://grafana.com/docs/grafana-cloud/send-data/otlp/send-data-otlp/).

### Tempo

Send OpenTelemetry traces to the Tempo OTLP Endpoint which supports both OTLP protocols: HTTP/Protobuf and gRPC.
