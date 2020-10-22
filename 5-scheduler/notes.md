# Scheduler

Every POD has a field nodename tha is not set by default. Kubernetes set it automatically. The scheduler goes through all the pods and look for those that do not have this property set. Then, the scheduler identifies the right node to the POD using the scheduling algorithm and set the nodename field. 

If there is no scheduler, the pods continue to be in Pending state. 

If the pod is already created, there is no way to set the nodename field. Instead, it is necessary to create a binding object and send a POST to the pods binding API with the data set to the binding object. 

## Labels and Selectors

Labels are properties atached to each item. Selectors allows to use filters based on these properties. 

## Annotations

Record details for information purpose.

## Taints and Tolerations

Taints and Tolerations are used to set restrictions on whats pods can be scheduled on a node. Taints are set on nodes as a specie of protection against pods, in order to block pods to be placed in this node. If necessary to put a pod in that node, we can add a toleration to the pod, a toleration for the taint of the node in which we want to add the pod. 

The taint-effect defines what happens to pods that not tolerate the taint. The options are:

* NoSchedule - The pods will not be schedule
* PreferNoSchedule - Try to not schedule the pod but it is not guaranteed.
* NoExecute - New pods are not schedule on the node. Existing pods will be evicted.

Taints and Tolerations does not tell the pod to go to an specific node. They only avoid the pod to be scehdule in some node. 

By default, the kubernetes sets a taint to the master node, that prevents any pods to be schedule to that node.

## Node Selectors

Limit a pod to run on a specific Node. 

## Node afinity

Provide advanced capabilities to limit pod placement on specific nodes. The node afinity is defined by key, value and operator. 

* Operator Equal - the afinity node label should be the same as specified in key value afinity
* Operator In - the node label can has the value of any of the specified in values afinity.
* Operator Exists - the afinity key should only exists on the node.

### Node afinity types

|        | DuringSchedule | DuringExecution |
|--------|----------------|-----------------|
| Type 1 | required       | Ignored         |
| Type 2 | Prefered       | Ignored         |
| Type 2 | Required       | Required        |

<br>

* Type 1 - The placement of the pod is crucial.
* Type 2 - The running of the pod is more important than its placement.
* Type 3 -The running pod pod is evicted or terminated if the node changes to a non afinity label. 

## Resource Requirement and Limits

Each node has a set of CPU, Memory and Disk resources available. The scheduler takes into consideration the amount of resources required by a pod and those available on the nodes. The default value for a POD is 0.5 CPU, 256 Mi. 

The resource required is the minimum amount of memory and CPU requested by the container when the scheduler tries to place the pod on that node.

0.5 CPU = 500m where m is mili. The minimum size is 1m. 1 count of CPU or 1000m is equivalente to 1 vCPU (AWS), 1 Core (GCP or Azure), 1 Hyperthread. 

For memory, Mi where Mi is Mebibyte, or G for Gibebyte. 1 Ki (Kibebyte) = 1024 bytes. 

Curiosity about the estabilishement of [Kibebyte](https://en.wikipedia.org/wiki/Kibibyte).

For the limit, kubernetes set 1vCPU and 512 Mi by default. A container cannot use more CPU than its limits. It does not happen with memory, the container can use more memory resources than its limit. If a POD tries to consume more memory than its limit constantly, the POD will be terminated. 

Tip: The status 'OOMKilled' indicates that the pod ran out of memory. Identify the memory limit set on the POD.

More details about kubernetes CPU limits can be found [here](https://medium.com/omio-engineering/cpu-limits-and-aggressive-throttling-in-kubernetes-c5b20bd8a718#:~:text=Kubernetes%20uses%20kernel%20throttling%20to,and%20it's%20easier%20to%20detect). 

# Daemon Sets

Daemon sets are like replica sets, but it runs one copy of a POD on each node of the cluster. The Daemon Set yaml definition is exactly the same of Replica Set definition, except for the Kind, that is Daemon Set. 

The Daemon Set uses Node Afinity to guarantee that every node will have a POD instance. 

# Static PODs

The kubelet can be configured to check a directory for files with pods definition files. So it is not necessary to have a Kubernetes API to deploy a new POD on the host. These PODS are noum as static PODs. That is possible because the kubelet works at a POD level.

Since static pods are not dependent on the kubernetes control plane, it is possible to use static pods to deploy the control plane components.

Both, Static pods and DaemonSet pods are ignored by the kube scheduler. 

The static PODs are defined by manifests stored at /etc/kubernetes/manifests folder. 

# Multiple Schedulers

It is possible to choose an personalized scheduler with an specific algorithm to choose the node to deploy a POD.