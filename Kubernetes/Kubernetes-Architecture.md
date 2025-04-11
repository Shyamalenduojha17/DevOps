---
# KUBERNETES ARCHITECTURE
![Screenshot (728)](https://github.com/Shyamalenduojha17/DevOps/assets/99936796/05303e16-adb6-44d2-a6b7-68c8233c9197)
---
### Cluster and Architecture

<details>
<summary>What is a Kubernetes Cluster?</summary><br><b>

Red Hat Definition: "A Kubernetes cluster is a set of node machines for running containerized applications. If you’re running Kubernetes, you’re running a cluster.
At a minimum, a cluster contains a worker node and a master node."

Read more [here](https://www.redhat.com/en/topics/containers/what-is-a-kubernetes-cluster)
</b></details>

<details>
<summary>What is a Node?</summary><br><b>

A node is a virtual or a physical machine that serves as a worker for running the applications.<br>
It's recommended to have at least 3 nodes in a production environment.
</b></details>

<details>
<summary>What the master node is responsible for?</summary><br><b>

The master coordinates all the workflows in the cluster:

* Scheduling applications
* Managing desired state
* Rolling out new updates

</b></details>

<details>
<summary>Describe shortly and in high-level, what happens when you run <code>kubectl get nodes</code></summary><br><b>

1. Your user is getting authenticated
2. Request is validated by the kube-apiserver
3. Data is retrieved from etcd
</b></details>

<details>
<summary>True or False? Every cluster must have 0 or more master nodes and at least 1 worker</summary><br><b>

False. A Kubernetes cluster consists of at least 1 master and can have 0 workers (although that wouldn't be very useful...)

</b></details> 

<details>
<summary>What are the components of the master node (aka control plane)?</summary><br><b>

  * API Server - the Kubernetes API. All cluster components communicate through it
  * Scheduler - assigns an application with a worker node it can run on
  * Controller Manager - cluster maintenance (replications, node failures, etc.)
  * etcd - stores cluster configuration

</b></details>

<details>
<summary>What are the components of a worker node (aka data plane)?</summary><br><b>

  * Kubelet - an agent responsible for node communication with the master.
  * Kube-proxy - load balancing traffic between app components
  * Container runtime - the engine runs the containers (Podman, Docker, ...)

</b></details>
