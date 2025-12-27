[<img src="https://vettom-images.s3.eu-west-1.amazonaws.com/logo/vettom-banner.jpg">](https://vettom.pages.dev/)

# Promshim for Httproutes and Ingress

Prometheus shim application to retrieve list of all Ingress, httproutes and present it in HTTP service Definition format for Prometheus to monitor.

## Access URL

App exposes ingress as well as HTTP routes

- http://<host>:<port>/ingress-sd # returns list of all ingress in HTTP service definition format
- http://<host>:<port>/httproutes-sd # returns list of all http routes in HTTP service definition format

#### Sample output

Following is the sample output for httproutes-sd endpoint in Prometheus service discovery format. Monitoring of URL can be automated using this SD format.

```json
[
  {
    "labels": {
      "__meta_application": "httproutes",
      "__meta_origin": "eks_cluster",
      "__meta_source": "prom_shim_http_routes"
    },
    "targets": ["prometheus.vettom.online", "grafana.vettom.online"]
  }
]
```

## Requirements

App uses prometheus service account role permission to list Ingresses and Http routes. During deployment, you must ensure that the ServiceAccount used by Pod can list all Ingresses across all namespaces.

## Build and push to Docker registry

```bash
podman build --platform linux/arm64,linux/amd64 .  -t dennysv/promshim-http-sd:<version>

podman push dennysv/promshim-http-sd:<version>
```
