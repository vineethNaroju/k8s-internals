*** About Me ***

- Master Nodes are the control plane for the cluster.
- If no masters are running or unable to reach a quorum, then cluster is
unable to scheudle and execute applications.
- Compute / Worker Nodes are disposable and can be added, removed very quickly from cluster.

*** Types ***

*** Single Master, Compute ***

- Easy for testing, proof-of-concepts, etc.
- No Availability if Master Node is fails and cluster can't exectue ops.

*** Multiple Master, Compute ***

- Master Nodes are deployed in 2N + 1 for quorum. 
- Each Master Node will maintain a copy of etcd database on itself.
- Elections will be held for "Kube-Controller-Manager" and "Kube-Scheduler"
leader to avoid conflicts.
- The Compute Nodes comms with any Master's APIserver via Load Balancer.

*** Master, Etcd, Compute ***

- Isolate Etcd cluster from other Master Server services.
- It reduces workload from Master Nodes, to be in smaller size and easy to
scale out.
- It increase complexity but improves support and management of Etcd.

*** Red Hat OpenShift Infra ***

- Infra nodes handle log aggregation, metrics collection, reporting,
container registry services, overlay network management and routing.
- Red Hat recommends at least 3 infra nodes for prod. 
- It enable to have additional redundancy, different CPU/RAM requirements, etc.
