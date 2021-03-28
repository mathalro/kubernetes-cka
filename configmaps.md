# Configmaps

## Imperative

k create configmap \
  app-config --from-literal=APP_COLOR=blue
  
k create configmap \
  app-config --from-file=appconfig.property
  
## Declarative

```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: app-config
data:
  APP_COLOR: blue
```

## Reference in a POD

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: pod
spec:
  containers:
  - envFrom:
      - configMapRef:
          name: app-config-map
    name: pod-example
    image: pod-example-image
```
