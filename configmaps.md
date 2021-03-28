# Configmaps

## Imperative

k create configmap \
  app-config --from-literal=APP_COLOR=blue
  
k create configmap \
  app-config --from-file=appconfig.property
  
## Declarative

```yaml
apiVersion: v1
metadata:
  name: app-config
data:
  APP_COLOR: blue
```
