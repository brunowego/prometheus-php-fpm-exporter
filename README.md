# prometheus-php-fpm-exporter

[php-fpm_exporter](https://github.com/hipages/php-fpm_exporter) is a Prometheus exporter for PHP-FPM metrics.

## TL;DR;

```sh
helm install stable/prometheus-php-fpm-exporter
```

## Introduction

This chart bootstraps a [php-fpm_exporter](https://github.com/hipages/php-fpm_exporter) deployment on a [Kubernetes](http://kubernetes.io) cluster using the [Helm](https://helm.sh) package manager.

## Prerequisites

- Kubernetes 1.8+ with Beta APIs enabled

## Installing the Chart

To install the chart with the release name `my-release`:

```sh
helm install --name my-release stable/prometheus-php-fpm-exporter
```

The command deploys `prometheus-php-fpm-exporter` on the Kubernetes cluster in the default configuration.

## Uninstalling the Chart

To uninstall/delete the `my-release` deployment:

```sh
helm delete my-release
```

The command removes all the Kubernetes components associated with the chart and deletes the release.

## Configuration

The following table lists the configurable parameters and their default values.

|             Parameter             |                                                              Description                                                              |            Default            |
| --------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------- |
| `replicaCount`                    | Desired number of `prometheus-php-fpm-exporter` replicas                                                                              | `1`                           |
| `image.repository`                | `prometheus-php-fpm-exporter` image repository                                                                                        | `hipages/php-fpm_exporter`    |
| `image.tag`                       | `prometheus-php-fpm-exporter` image tag                                                                                               | `1.0`                         |
| `image.pullPolicy`                | `prometheus-php-fpm-exporter` image pull policy                                                                                       | `IfNotPresent`                |
| `service.type`                    | Desired service type                                                                                                                  | `ClusterIP`                   |
| `service.internalport`            | Service listening port                                                                                                                | `9419`                        |
| `service.externalPort`            | Public service port                                                                                                                   | `9419`                        |
| `resources`                       | CPI/Memory resource requests/limits                                                                                                   | `{}`                          |
| `phpFpm.webListenAddress`         | Address on which to expose metrics and web interface                                                                                  | `:9253`                       |
| `phpFpm.webTelemetryPath`         | Path under which to expose metrics                                                                                                    | `/metrics`                    |
| `phpFpm.scrapeUri`                | FastCGI address, e.g. `unix:///tmp/php.sock;/status` or `tcp://127.0.0.1:9000/status`                                                 | `tcp://myphp-fpm:9000/status` |
| `phpFpm.fixProcessCount`          | Enable to calculate process numbers via `php-fpm_exporter` since PHP-FPM sporadically reports wrong active/idle/total process numbers | `false`                       |
| `phpFpm.logLevel`                 | Only log messages with the given severity or above. Valid levels: [debug, info, warn, error, fatal] (default "error")                 | `info`                        |
| `podAnnotations`                  | Pod annotations for easier discovery                                                                                                  | `{}`                          |
| `serviceMonitor.enabled`          | Enable Prometheus Operator ServiceMonitor monitoring                                                                                  | `false`                       |
| `serviceMonitor.additionalLabels` | Additional labels that can be used so ServiceMonitor will be discovered by Prometheus                                                 | `{}`                          |
| `serviceMonitor.interval`         | Interval at which Prometheus Operator scrapes exporter                                                                                | `15s`                         |
| `serviceMonitor.namespace`        | Define namespace where to deploy the ServiceMonitor resource                                                                          | `[]`                          |

For more information please refer to the [php-fpm_exporter](https://github.com/hipages/php-fpm_exporter) documentation.

Specify each parameter using the `--set key=value[,key=value]` argument to `helm install`. For example,

```sh
helm install --name my-release \
  --set "phpFpm.scrapeUri=tcp://myphp-fpm:9000/status" \
    stable/prometheus-php-fpm-exporter
```

Alternatively, a YAML file that specifies the values for the parameters can be provided while installing the chart. For example,

```sh
helm install --name my-release -f values.yaml stable/prometheus-php-fpm-exporter
```
