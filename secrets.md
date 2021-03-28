# Secrets

Secrets can be used like configmap to store environment varibles but for sensitive information.

## Imperative

```sh
k create secret generic \
  app-secret --from-literal=DB_HOST=mysql
```
