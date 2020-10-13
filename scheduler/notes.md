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