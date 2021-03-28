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
metadata:
  name: generic
data:
  DB_HOST: mysql
```

## Encoding data

```sh
echo -n 'value-to-encode' | base64 --encode 
```
