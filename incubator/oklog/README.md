# Oklog

> OK Log is a distributed and coördination-free log management system for big ol' clusters. It's an on-prem solution that's designed to be a sort of building block: easy to understand, easy to operate, and easy to extend.

# Is OK Log for me?

> You may consider OK Log if...
> 
> - You're tailing your logs manually, find it annoying, and want to aggregate them without a lot of fuss
> - You're using a hosted solution like Loggly, and want to move logs on-prem
> - You're using Elasticsearch, but find it unreliable, difficult to operate, or don't use many of its features
> - You're using a custom log pipeline with e.g. Fluentd or Logstash, and having performance problems
> - You just wanna, like, grep your logs — why is this all so complicated?

# Prerequesites

* Kubernetes 1.4+ with Beta APIs enabled
* PV provisioner support in the underlying infrastructure

# Install

Run

```
helm install incubator/oklog --name=my-release-name
```

to install oklog with the release name `my-release-name`.

# Uninstall

```
helm delete incubator/oklog [--purge]
```

Specifying the `--purge` option will delete persistence storage volumes and will not remember any previous configuration.

# Configuration

| Parameter | Description | Default |
|-----------|-------------|---------|
| `image` | The docker image to pull (without tag). | `"oklog/oklog"` |
| `imageTag` | The docker image version. | `v0.2.1` |
| `imagePullPolicy` | When to pull the docker image. | `"Always"` |
| `replicas` | How many replicas to create initially. | `4` |
| `ingress.enabled`| Use an ingress to expose the Web UI | `false` |
| `ingress.host` | The hostname to use for this ingress | `"oklog.example.com"` |
| `ingress.annotations` | The annotation configuration for the ingress (YAML). | `{}` |
| `ingress.tls` | The TLS configuration for the ingress (YAML). | `[]` |
| `persistence.enabled` | Is persistence storage enabled? If set to false, `emptyDir: {}` will be used. | `true` |
| `persistence.accessMode` | [ReadWriteOnce/ReadWriteMany/ReadOnlyMany](https://kubernetes.io/docs/concepts/storage/persistence-volumes/#access-modes) | `"ReadWriteOnce"` |
| `persistence.size` | How large the persistence Volume should be. | `1Gi` |
| `resources.requests.memory` | How much memory to allocate for each oklog pod. | `128Mi` |
| `resources.requests.cpu` | The fraction of a CPU core to allocate to each oklog pod. | `0.1` |

