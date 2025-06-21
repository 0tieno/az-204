# KCNA Notes

---

## Continuous Integration and Delivery

- **Continuous Integration (CI):**
  - The first part of the process.
  - Describes the permanent building and testing of the written code.

- **Continuous Delivery (CD):**
  - The second part of the process.
  - Automates the deployment of the pre-built software.

---

## GitOps Frameworks

- **Popular Pull-Based GitOps Frameworks:**
  - **Flux:** Built with the GitOps Toolkit (a set of APIs and controllers used to extend Flux or build custom delivery platforms).
  - **ArgoCD:** Implemented as a Kubernetes controller.

---

## Observability

Observability should provide answers to questions such as:

- Is the system stable or does it change its state when manipulated?
- Is the system sensitive to change (e.g., do some services have high latency)?
- Do certain metrics in the system exceed their limits?
- Why does a request to the system fail?
- Are there any bottlenecks in the system?

---

### Three Data Categories

- **Logs**
- **Metrics**
- **Traces**

#### Methods to Ship Logs

- **Node-level logging:**  
  The most efficient way. Admin configures a log shipping tool to collect and send logs to a central store.
- **Logging via sidecar container:**  
  A sidecar container collects and ships logs to a central store.
- **Application-level logging:**  
  The application pushes logs directly to the central store. Convenient, but requires configuring every app in the cluster.

#### Prometheus Data Model - Four Core Metrics

- **Counter:** Value that increases (e.g., request or error count).
- **Gauge:** Value that increases or decreases (e.g., memory size).
- **Histogram:** Sample of observations (e.g., request duration).
- **Summary:** Like a histogram, but also provides the total count of observations.

- **Trace:**  
  Describes the tracking of a request as it passes through services.

---

## Kubernetes Architecture

- **Kubernetes Cluster:**  
  Spans multiple servers for load distribution and task separation.

### Node Types

- **Control Plane Node(s):**  
  The brains of Kubernetes. Manages the cluster and tasks like deployment, scheduling, and self-healing.
- **Worker Nodes:**  
  Where applications run. No further logic implemented; behavior is controlled by the control plane.

### Namespaces

- Used to divide a cluster into multiple virtual clusters.
- Useful for multi-tenancy.
- Not suitable for strong isolation; think of namespaces like directories in a filesystem.

---

### Control Plane Node Components

- **kube-apiserver:**  
  Central component; all others interact with it. User access point.
- **etcd:**  
  Database holding cluster state. Standalone project, not part of Kubernetes proper.
- **kube-scheduler:**  
  Chooses worker nodes for workloads based on resource properties.
- **kube-controller-manager:**  
  Runs control loops to maintain desired cluster state.
- **cloud-controller-manager (optional):**  
  Interacts with cloud provider APIs for external resources.

---

### Worker Node Components

- **Container Runtime:**  
  Runs containers (e.g., containerd, CRI-O, Docker).
- **kubelet:**  
  Agent on every worker node. Talks to API server and container runtime to start containers.
- **kube-proxy:**  
  Network proxy for cluster communication. Relies on OS networking when possible.

---

## Kubernetes API

- The most important component.
- All communication (users/components) requires the API server.

---

## Pods

- Smallest deployable unit.
- Wrapper around one or more containers.
- Containers in a pod share IP and filesystem.

---

### Pod Lifecycle Phases

- **Pending:**  
  Pod accepted but containers not ready.
- **Running:**  
  Bound to node; at least one container running or starting/restarting.
- **Succeeded:**  
  All containers terminated successfully; will not restart.
- **Failed:**  
  All containers terminated, at least one with failure.
- **Unknown:**  
  State can't be obtained due to error.

---

## Kubernetes Objects

- **ReplicaSet:**  
  Ensures a desired number of pods are running. Used for scaling and availability.
- **Deployment:**  
  Manages app lifecycle via ReplicaSets. Ideal for stateless apps.
- **StatefulSet:**  
  For stateful applications (e.g., databases). Retains pod IPs, provides stable identities/persistent storage.
- **DaemonSet:**  
  Ensures a pod runs on all/some nodes (e.g., for logging/monitoring).
- **Job:**  
  Creates pods for tasks that terminate after execution (e.g., migrations).
- **CronJob:**  
  Schedules jobs on a time-based basis (e.g., nightly backups).

---

## Kubelet

- Primary node agent running on each node.
- Monitors application servers and routes admin requests.

---

## Configurations: ConfigMap

- Decouples configuration from Pods.
- Stores config files or variables as key-value pairs.

---

## Container Runtimes

- **containerd**
- **CRI-O**
- **Docker**

---

## Kubernetes Networking Problems

1. **Container-to-Container:**  
   Solved by the Pod concept.
2. **Pod-to-Pod:**  
   Solved with overlay networks.
3. **Pod-to-Service:**  
   Handled by kube-proxy and node packet filter.
4. **External-to-Service:**  
   Handled by kube-proxy and node packet filter.

### Networking Requirements

- All pods can communicate across nodes.
- All nodes can communicate with all pods.
- No Network Address Translation (NAT).

---

## Scheduling

- Sub-category of orchestration.
- Automatically chooses the right node for workloads.
- **kube-scheduler** makes decisions but does not start workloads.

---

## Helm

- Package manager for Kubernetes.
- Packages objects into Charts for sharing and easier updates.

---
