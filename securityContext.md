# Security Context

Security context are used to limit the user permissions.

## POD

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: pod-security
spec:
  containers:
    - name: pod-security-container
      image: pod-security
      securityContext:
        runAsUser: 1010
        capabilities:
          add: ["SYS_TIME"]
```
