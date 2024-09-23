# Certified Kubernetes Administrator

## Kubeconfig


Kubeconfig contains the configuration required for user authentication, authorization, and the permissions to communicate with the Kubernetes API server.

It is located in the .kube directory. On a Mac, the path would be:

```
vim /Users/<username>/.kube/config
```

The structure of Kubeconfig is similar to a Kubernetes manifest, with fields like apiVersion. Under the **clusters** section, there is a **cluster** object, which includes a subfield called **certificate-authority-data**. This field is responsible for authenticating the user with the cluster.

Additionally, the **server** field defines the full domain name for accessing the cluster, while the **name** field under clusters provides the cluster's identifier.

After the cluster information (or clusters if you are working with multiple clusters), there is a section called **contexts**. This section includes a sub-field named **context**, which enables you to connect to different clusters.

Note: The cluster you are currently connected to is specified by the **current-context** field.

Next, you have the user information, which defines how you authenticate with the clusters. The most crucial part of this section is the **client-certificate** information, as it determines the user's authentication, authorization, and permissions to interact with the cluster.

## Kubernetes Control Plane and Worker node breakdown (high level).

| Control Plane Component | Worker Node Component |
| ----------------------- | --------------------- |
| API Server: API is used to connect to kubernetes and deploy workload. | Kubelet: Kubernetes agent. |
| ETCD: ETCD is the database for kubernetes and it store any non-ephemeral data. | Kube-proxy: Does the internal networking for the Kubernetes. |
| Scheduler: Deploys the pods onto the desired worker node. | CRI: Container runtime interface. Kubernetes inherently dosen't know how to run containers and hence it uses CRI plugin to provide the runtime environment for containers. |
| Controller: Confirms the current states is the desired state of all the running workloads. | CoreDNS: CoreDNS handles all the dns capabilites inside the Kubernetes. |

**Note: The recommended number of control plane nodes is 3, primarily due to ETCD. ETCD uses an algorithm called RAFT, which requires leader election— a process to determine which control plane node serves as the leader at any given time.**



