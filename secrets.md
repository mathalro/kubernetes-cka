# Secrets

Secrets can be used like configmap to store environment varibles but for sensitive information.

## Imperative

```sh
k create secret generic \
  app-secret --from-literal=DB_HOST=mysql
```

## Declarative

```yaml
apiVersion: v1
kind: Secret
metadata:
  name: generic
data:
  DB_HOST: mysql
```

## Encoding data

```sh
echo -n 'value-to-encode' | base64 --encode 
```

## Referencing secret in a POD

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: pod
spec:
  containers:
  - envFrom:
      - secretRef:
          name: app-secret
    name: pod-example
    image: pod-example-image
```
