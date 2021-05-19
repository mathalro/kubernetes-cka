# Usefull Commands Kubectl

## Explain

You do not need to decorate the structure for each resource in kubernetes. You just need to know how to use the explain command. With this command you can undesrtand what is necessary to create a new resource and how to create it. 

### Explain a pod

The command:

```sh
kubectl explain pod --recursive
```

will return all the necessary structure for a pod Workload. Whats is required, what is the object type and etc.