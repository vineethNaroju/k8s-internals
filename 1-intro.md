*** Master Node ***

- More than one Master Node for High Availability and with one leader to
perform all the operations. Remaining Master Nodes follow this leader.
- To manage cluster state, we use etcd as distributed key value store.

- APIserver <> etcd 
- APIserver <> Controller
- APIserver <> Scheduler

*** Kube API Server ***

- kubectl is used to communicate with APIserver.
- It stores cluster information on Etcd.
- It scales horizontally and is front end for k8s control plane.

*** Kube Scheduler ***

- It has resource usage info for each worker node.
- It schedules pods and service onto different worker nodes.
- It also considers quality of service, data locality, etc.

- It watches for newly created Pods with no assigned node and selects
a node for them to run on.

*** Kube Controller Manager ***

- Non-terminating control loops regulate the state of k8s cluster. Each of
these control loops know about desired state of objects it manages.
- It fetches current state from APIserver and takes necessary steps to get
closer to desired state.

- It runs Controller processes, each controller is a separate process but
to reduce complexity - it's compiled to single binary and run in single process.
- Node controller: Notices and responds when nodes go down.
- Job controller: Watches for Job objects that represent one-off tasks,
then creates pods to run those tasks to completion.
- Endpoints controller: Populates the Endpoionts objects (joins Services &
Pods).
- Service Account & Token controllers: Create default accounts and API access tokens for new namespacess.


*** Cloud Controller Manager ***

- Cloud specific control logic and runs controllers specific to provider.
- Route controller, Service controller (CUD cloud load balancers)


*** Etcd ***

- Distributed key-value store used to store the cluster state.
- It's coded in Go and based on Raft consensus algo.
- One of the Nodes will be Master and remaining are Followers.
- It's also used to store config details like subnets, ConfigMaps, etc.
- It's either part of K8s Master or configured externally.

*** Worker Node ***

- A virtual or physical server that runs pods. Pods are scheduled on worker
nodes. 
- To access applications, you have to connect to worker nodes and not master node.

- Container Runtime
- Kubelet
- Kube-Proxy

*** Container Runtime ***

- It manages life cycle of containers on worker nodes.
- Ex like rkt, lxc, docker.

*** Kubelet ***

- Agent that runs on each Worker Node and comms with Master Node.
- It receives pod definitio and runs that container associated with it.
- It makes sure that containers are always healthy.
- It connects with Container Runtime using gRPC to perform container
and image operations.
- We have Imgae Service for image ops and Runtime Service to manage 
pod and container ops.
- With Docker, containers are created using docker on Worker Node and 
internally docker uses container to create and manage them.


*** Kube Proxy ***

- Runs on each Worker Node as Network Proxy.
- It listens to APIserver for service point creation or deletion.
- It manages serivce routes (?)

- It maintains network rules and allow comms to Pods from network.
- It uses OS packet filtering otherwse just forwards traffic itself.

*** Addons ***

- They use k8s resources (DaemonSet, Deployment, etc) for cluster features.
- These are namespaced resources and belong to kube-system namespace.

*** DNS ***

- All k8s cluster should have cluster DNS.

*** Dashboard ***

- UI for clusters.





