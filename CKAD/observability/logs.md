# Log

To get logs in kubernetes is pretty simple:

```sh
kubectl logs pod-name
```

It is possible get the logs from some time period, like:

```sh
kubectl logs pod-name --since=10s
```

that get the last 10 seconds logs.

## Multi container

For multicontainer, it is necessary to specify which container you want to see the logs. 

```sh
kubectl logs pod-name container-name
```

or get the logs for all containers

```sh
kubectl logs pod-name --all-containers=true
```



