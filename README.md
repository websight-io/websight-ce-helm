# WebSight Charts
![Version: 1.2.0](https://img.shields.io/badge/Version-1.2.0-informational?style=flat-square) ![Type: application](https://img.shields.io/badge/Type-application-informational?style=flat-square) ![AppVersion: 1.6.0](https://img.shields.io/badge/AppVersion-1.6.0-informational?style=flat-square)

This chart bootstraps WebSight CMS deployment on a Kubernetes cluster using the Helm package manager.

[WebSight](https://websight.io/) is a Digitial Experience Platform driven by the enterprise-grade CMS.

## Prerequisites

- Kubernetes cluster with at least 8 GB ram and 2 CPU
- Ingress installed on k8s cluster (you may use e.g. [Nginx ingress](https://kubernetes.github.io/ingress-nginx/deploy/)).
- Helm 3.6+

## CMS

### Quick start
```bash
helm upgrade --install my-websight websight-cms \
  --repo https://websight-io.github.io/charts \
  --namespace ws --create-namespace --set ingress.enabled=true
```

> WebSight instance will be available at:
> - CMS Panel: http://cms.127.0.0.1.nip.io
> - Demo sites:
>   - http://luna.127.0.0.1.nip.io
>   - http://bulma-personal-template.127.0.0.1.nip.io
>   - http://no-code.luna.127.0.0.1.nip.io

### Installing the Chart
To install the chart with the release name `my-websight` using existing domain that points to your Kubernetes cluster, run:
```bash
helm repo add websight https://websight-io.github.io/charts
helm install --set ingress.enabled=true --set ingress.hosts.cms=cms.my-page.domain --set ingress.hosts.sites={'my-page.domain'} my-websight websight/websight-cms -n ws --create-namespace
```

This command deploys WebSight CE on Kubernetes cluster with the default configuration using `ws` namespace.
The [Parameters](#parameters) section lists the parameters that can be configured.

### Uninstalling the Chart
To uninstall/delete the deployment run:
```bash
helm uninstall my-websight -n ws
```

The command removes all the Kubernetes components associated with the chart and deletes the release.

### Parameters
| Key | Type | Default | Description |
|-----|------|---------|-------------|
| cms.env | list | `[{"name":"LEASE_CHECK_MODE","value":"LENIENT"},{"name":"WS_ADMIN_USERNAME","value":"wsadmin"}]` | WebSight CMS environment variables |
| cms.envsFrom | list | `[]` | List of WebSight CMS config maps that will work with `configMapRef` |
| cms.image.pullPolicy | string | `"IfNotPresent"` | WebSight CMS project image pull policy |
| cms.image.repository | string | `"public.ecr.aws/ds/websight-cms-starter"` | WebSight CMS project image repository |
| cms.image.tag | string | `"1.6.0"` | WebSight CMS project image tag |
| cms.livenessProbe.enabled | bool | `true` | enables WebSight CMS pods liveness probe |
| cms.livenessProbe.failureThreshold | int | `3` |  |
| cms.livenessProbe.initialDelaySeconds | int | `30` |  |
| cms.livenessProbe.periodSeconds | int | `10` |  |
| cms.livenessProbe.successThreshold | int | `1` |  |
| cms.livenessProbe.timeoutSeconds | int | `3` |  |
| cms.ports.panel | int | `8080` | CMS Panel port |
| cms.readinessProbe.enabled | bool | `true` | enables WebSight CMS pods readiness probe |
| cms.readinessProbe.failureThreshold | int | `3` |  |
| cms.readinessProbe.initialDelaySeconds | int | `30` |  |
| cms.readinessProbe.periodSeconds | int | `30` |  |
| cms.readinessProbe.successThreshold | int | `1` |  |
| cms.readinessProbe.timeoutSeconds | int | `10` |  |
| cms.replicas | int | `1` | number of WebSight CMS replicas |
| cms.resources.limits.cpu | string | `"1000m"` | WebSight CMS limits cpu resources |
| cms.resources.limits.memory | string | `"4Gi"` | WebSight CMS limits memory resources |
| cms.resources.requests.cpu | string | `"500m"` | WebSight CMS request cpu resources |
| cms.resources.requests.memory | string | `"1Gi"` | WebSight CMS request memory resources |
| ingress.enabled | bool | `false` | enables ingress |
| ingress.hosts.cms | string | `"cms.127.0.0.1.nip.io"` | cms panel host |
| ingress.hosts.sites | list | `["luna.127.0.0.1.nip.io","bulma-personal-template.127.0.0.1.nip.io","no-code.luna.127.0.0.1.nip.io"]` | demo sites hosts |
| mongo.env | list | `[{"name":"MONGO_INITDB_ROOT_PASSWORD","value":"mongoadmin"},{"name":"MONGO_INITDB_ROOT_USERNAME","value":"mongoadmin"}]` | MongoDB Content Store environment variables |
| mongo.image.pullPolicy | string | `"IfNotPresent"` | MongoDB Content Store image pull policy |
| mongo.image.repository | string | `"mongo"` | MongoDB Content Store image repository |
| mongo.image.tag | string | `"4.4.6"` | MongoDB Content Store image tag |
| mongo.livenessProbe.enabled | bool | `true` | enables MongoDB pods liveness probe |
| mongo.livenessProbe.failureThreshold | int | `3` |  |
| mongo.livenessProbe.initialDelaySeconds | int | `15` |  |
| mongo.livenessProbe.periodSeconds | int | `10` |  |
| mongo.livenessProbe.successThreshold | int | `1` |  |
| mongo.livenessProbe.timeoutSeconds | int | `5` |  |
| mongo.ports.service | int | `27017` | MongoDB Content Store port |
| mongo.resources.limits.cpu | string | `"1000m"` | MongoDB limits cpu resources |
| mongo.resources.limits.memory | string | `"4Gi"` | MongoDB limits memory resources |
| mongo.resources.requests.cpu | string | `"500m"` | MongoDB request cpu resources |
| mongo.resources.requests.memory | string | `"1Gi"` | MongoDB request memory resources |
| mongo.storage.size | string | `"2Gi"` | MongoDB Repository volume size |
| nginx.enabled | bool | `true` | enables Web Server |
| nginx.env | list | `[]` | WebSight Nginx environment variables |
| nginx.image.pullPolicy | string | `"IfNotPresent"` | Web Server image pull policy |
| nginx.image.repository | string | `"public.ecr.aws/ds/websight-nginx-starter"` | Web Server image repository |
| nginx.image.tag | string | `"1.6.0"` | Web Server project image tag |
| nginx.livenessProbe.enabled | bool | `true` | enables WebSight Nginx pods liveness probe |
| nginx.livenessProbe.failureThreshold | int | `6` |  |
| nginx.livenessProbe.initialDelaySeconds | int | `30` |  |
| nginx.livenessProbe.periodSeconds | int | `5` |  |
| nginx.livenessProbe.successThreshold | int | `1` |  |
| nginx.livenessProbe.timeoutSeconds | int | `1` |  |
| nginx.ports.http | int | `80` | Nginx port |
| nginx.replicas | int | `2` | number of Web Server replicas |
| nginx.resources.limits.cpu | string | `"100m"` | WebSight Nginx limits cpu resources |
| nginx.resources.limits.memory | string | `"100Mi"` | WebSight Nginx limits memory resources |
| nginx.resources.requests.cpu | string | `"50m"` | WebSight Nginx request cpu resources |
| nginx.resources.requests.memory | string | `"50Mi"` | WebSight Nginx request memory resources |
| siteRepository.enabled | bool | `true` | enables Site Repository volume |
| siteRepository.rwxStorageClassName | string | `nil` | Configure storageClassName in case you want to use `ReadWriteMany` access mode |
| siteRepository.storage.size | string | `"2Gi"` | Site Repository volume size |

## Improvements (help wanted)

- configmaps/secrets support
- ingress support for cloud providers (`metadata.annotations`)
- `*` use mongo from bitnami