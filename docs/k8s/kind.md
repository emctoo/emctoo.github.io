

### [advanced](https://kind.sigs.k8s.io/docs/user/quick-start/#advanced)

Use a config yaml file

```yaml
kind create cluster --config kind-config-example.yaml
```

#### multi-node cluster

```yaml
kind: Cluster
apiVersion: kind.x-k8s.io/v1alpha4
nodes:
- role: control-plane
- role: worker
- role: worker
```

