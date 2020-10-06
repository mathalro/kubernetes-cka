## Imperative

Say what is required and how to get the things done.

### K8s imperative examples

k run --image=nginx nginx
k create deployment --image=nginx nginx
k expose deployment nginx --port 80
k edit deployment nginx
k scale deployment nginx --replicas=5
k set image deployment nginx nginx=nginx:1.18

### k8s imperative configuration files examples

#### create

k create -f nginx.yaml

#### update

k edit deployment nginx - change not recorded anywhere
k replace -f nginx.yaml - update the image after update the local file. Fails if object does not exists
k replace --force -f nginx.yaml - update objects - completly delete and recreate objects
k create -f nginx.yaml - fails if the object already exists.

## Declarative

Say what is required, but not how to do.

### Declarative K8s examples

kubectl apply -f nginx.yaml - inteligent enough to create an object if it does not aleready exists and to update it if it already exists.
