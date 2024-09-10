# Kubernetes

Kubernetes (often abbreviated as K8s) is an open-source platform designed to automate deploying, scaling, and operating containerized applications. It helps manage clusters of containers, ensuring that applications run smoothly across different environments, whether on-premise or in the cloud.

Here’s a simplified overview of Kubernetes:

### Key Concepts:

1. **Containers**: These are lightweight, isolated environments (usually using Docker) that package applications and their dependencies.
2. **Cluster**: Kubernetes operates in a cluster environment, which is a group of nodes (machines) that can either be physical or virtual. The cluster is managed by Kubernetes to run containers.

3. **Pods**: A pod is the smallest deployable unit in Kubernetes. It usually contains one or more containers that share storage, network resources, and a specification for how to run the containers.

4. **Nodes**: A node is a worker machine in Kubernetes (can be a VM or physical machine). Each node contains the services necessary to run the containers.

5. **Master Node**: This controls the cluster and manages all the worker nodes. It ensures that the desired number of containers are running and takes care of scaling, scheduling, and updates.

6. **Service**: A service in Kubernetes defines a set of Pods and a policy to access them (such as load balancing).

7. **Deployment**: A Deployment is a Kubernetes object that manages stateless applications. It helps you define how many replicas (copies) of an application you want running, and Kubernetes will handle making sure that number is maintained.

8. **Scaling**: Kubernetes makes it easy to scale up or down the number of replicas of an application automatically based on the workload.

### Main Features of Kubernetes:

1. **Automatic Bin Packing**: Kubernetes can automatically place containers across your cluster based on resource needs, balancing efficient use of the cluster.

2. **Self-Healing**: If a container crashes, Kubernetes automatically restarts it or replaces it, making applications more resilient.

3. **Service Discovery and Load Balancing**: Kubernetes assigns IP addresses and a DNS name to each pod and distributes traffic across them, providing easy service discovery and load balancing.

4. **Horizontal Scaling**: Kubernetes allows you to scale your applications up or down seamlessly based on demand.

5. **Storage Orchestration**: Kubernetes can automatically mount storage systems like local storage, cloud providers (AWS, GCP), or network storage systems.

6. **Automated Rollouts and Rollbacks**: Kubernetes can automatically roll out new versions of applications and roll back changes if there’s an issue.

7. **Secret and Configuration Management**: It can manage sensitive information, such as passwords or API tokens, without exposing them in your application’s code.

### Use Cases for Kubernetes:

- **Cloud-Native Applications**: It’s perfect for modern, microservices-based apps.
- **Hybrid Cloud**: Can manage applications across multiple environments (on-premise, public cloud).
- **High Availability**: Automatically restarts failing containers or reschedules them on different nodes.
- **Continuous Integration/Delivery (CI/CD)**: Supports automating application deployment pipelines.

Kubernetes has become the industry standard for managing containerized applications at scale, making it easier to build, deploy, and manage applications in a consistent way.

### The Kubernetes API

The **Kubernetes API** is the central interface used to interact with a Kubernetes cluster. It provides a way for users, external applications, and internal components to communicate with and manage resources within the Kubernetes ecosystem.

Everything in Kubernetes — from creating Pods, scaling applications, monitoring health, to managing networks — happens through the Kubernetes API. The API enables automation and integration with external systems, making Kubernetes highly extensible.

### Key Features of the Kubernetes API

1. **Declarative Model**: Kubernetes API is declarative. This means you define the desired state (e.g., you declare that you want 5 replicas of a Pod), and Kubernetes ensures the current state matches the desired state.
2. **RESTful Interface**: The Kubernetes API is REST-based, allowing communication through standard HTTP methods like `GET`, `POST`, `PUT`, and `DELETE`.

3. **Resource Management**: All Kubernetes objects (e.g., Pods, Services, Deployments) are represented as resources that can be created, updated, or deleted through API requests.

4. **Versioned API**: The Kubernetes API supports different versions (e.g., v1, v1beta1) to ensure backward compatibility and to allow for phased improvements and new features.

### Common Kubernetes API Objects (Resources)

1. **Pod**: Represents a running instance of one or more containers.
2. **Service**: Defines how to expose an application running on a set of Pods.
3. **Deployment**: Manages the lifecycle of Pods, including scaling, rolling updates, and rollbacks.
4. **Namespace**: Provides isolation between different environments or teams in the same Kubernetes cluster.
5. **ConfigMap**: Stores configuration data that can be injected into Pods.
6. **Secret**: Stores sensitive data like passwords and tokens securely.

### Basic API Operations

- **Create**: Use `POST` to create resources.
- **Read**: Use `GET` to retrieve information about resources.
- **Update**: Use `PUT` or `PATCH` to modify existing resources.
- **Delete**: Use `DELETE` to remove resources.

For example, to get all the running Pods in a cluster, you would use the following API call:

```
GET /api/v1/pods
```

### Example: Using `kubectl` to Interact with the API

`kubectl` is the command-line tool that interacts with the Kubernetes API. It abstracts the API calls into a more user-friendly interface.

- **Get all Pods**:

  ```bash
  kubectl get pods
  ```

- **Describe a Pod**:

  ```bash
  kubectl describe pod <pod-name>
  ```

- **Create a resource from a YAML file**:

  ```bash
  kubectl apply -f pod.yaml
  ```

- **Delete a resource**:
  ```bash
  kubectl delete pod <pod-name>
  ```

### Example of Kubernetes API Request

A simple `curl` command can be used to make direct API requests (e.g., to get information about nodes):

```bash
curl -X GET https://<kubernetes-master-ip>/api/v1/nodes -H "Authorization: Bearer <token>"
```

### Authentication and Security

- **Authentication**: API requests must be authenticated. Kubernetes supports several authentication mechanisms, including tokens, client certificates, and OpenID Connect.
- **Authorization**: After authentication, Kubernetes determines if the user or system making the API request has the necessary permissions using Role-Based Access Control (RBAC).

- **Admission Control**: Before a request can be persisted, admission controllers can enforce certain rules, such as resource quotas or policy enforcement.

### API Versions and Stability

The Kubernetes API evolves over time. The API is divided into three stability levels:

- **Alpha**: Experimental features, may be subject to breaking changes.
- **Beta**: More stable but still in development, changes may happen but are less frequent.
- **Stable (v1)**: Fully supported and backward-compatible features.

### Working with API Resources

Kubernetes objects are defined in YAML or JSON format. For instance, a simple Pod definition:

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: my-pod
spec:
  containers:
    - name: nginx-container
      image: nginx
```

You can apply this resource using the Kubernetes API via `kubectl apply -f pod.yaml` or by making an HTTP request to the API.

### Conclusion

The Kubernetes API is a powerful interface for interacting with and managing Kubernetes resources. Whether you're using `kubectl`, integrating external services, or automating tasks, understanding the Kubernetes API is fundamental to effectively working with Kubernetes.

# Kubernetes Architecture

Docs : https://kubernetes.io/docs/concepts/architecture/

![alt text](/Images/image26.png)

### Kubernetes Cluster Architecture

A Kubernetes cluster is a set of machines (called **nodes**) that run containerized applications managed by Kubernetes. It provides a scalable, resilient, and flexible platform for deploying, managing, and scaling applications. Below is an explanation of the key components of the Kubernetes cluster architecture:

---

### 1. **Master Node (Control Plane)**

The master node is the brain of the Kubernetes cluster. It manages the cluster, schedules applications, and ensures the desired state of the system.

**Key Components of the Master Node**:

- **API Server (kube-apiserver)**:

  - **Description**: The API server is the entry point for all administrative tasks in a Kubernetes cluster. It exposes the Kubernetes API, which is used by users and components to communicate.
  - **Role**: Validates and processes requests (e.g., creating or scaling applications) and updates the cluster state in the etcd database.

- **etcd**:

  - **Description**: A distributed key-value store that stores all the cluster’s data, including configuration, state, and metadata.
  - **Role**: Acts as the source of truth for the cluster state, providing fault tolerance and consistency across the system.

- **Controller Manager (kube-controller-manager)**:

  - **Description**: A collection of controllers that handle routine tasks in the cluster, such as ensuring that the desired number of pods are running.
  - **Role**: Manages replication, scaling, node monitoring, and other background processes to maintain the desired state of the cluster.

- **Scheduler (kube-scheduler)**:
  - **Description**: Responsible for assigning new workloads (Pods) to nodes.
  - **Role**: Schedules Pods to run on specific nodes based on resource availability and policies like resource requests, constraints, or affinity rules.

---

### 2. **Worker Nodes (Compute Nodes)**

Worker nodes run the application workloads (i.e., containers). Each node in the cluster hosts Pods and communicates with the master node to get instructions about workloads.

**Key Components of Worker Nodes**:

- **Kubelet**:

  - **Description**: An agent that runs on each worker node and communicates with the control plane.
  - **Role**: Ensures that containers in Pods are running as expected. It interacts with the container runtime to start and manage containers.

- **Container Runtime**:

  - **Description**: Software responsible for running containers. The most common runtime is Docker, but Kubernetes supports others like containerd and CRI-O.
  - **Role**: Manages the lifecycle of containers (e.g., starting, stopping, and removing containers).

- **Kube-proxy**:
  - **Description**: A network proxy that runs on each node to manage networking rules.
  - **Role**: Ensures that network traffic reaches the appropriate Pods by maintaining the network rules for Pods and Services, including load balancing.

---

### 3. **Pods**

- **Description**: The smallest deployable unit in Kubernetes, which can run one or more containers. Each Pod is assigned an IP address and runs in an isolated environment.
- **Role**: Hosts the application containers, sharing networking and storage within the Pod.

---

### 4. **Networking**

- **Service**:

  - **Description**: A Kubernetes object that exposes Pods to the network, allowing external or internal traffic to reach them.
  - **Role**: Provides a stable network interface for communication, load balancing traffic to the appropriate Pods.

- **Overlay Network**:
  - **Description**: A virtual network that spans all nodes, allowing communication between Pods on different nodes.
  - **Role**: Enables Pods across nodes to communicate seamlessly by abstracting the underlying infrastructure.

---

### Cluster Communication

- **Control Plane to Nodes**: The control plane (master) communicates with nodes to schedule workloads and monitor their state.
- **Pods to Pods**: Pods can communicate with each other across the cluster using Kubernetes networking.

---

### Diagram Overview:

1. **Master Node**: Manages the cluster state, schedules workloads, and handles API requests.
2. **Worker Nodes**: Execute application workloads by running Pods.
3. **Pods**: Containers grouped together, running the application services.
4. **Networking**: Provides communication between different components of the cluster and external traffic.

Together, these components create a powerful orchestration system that can automatically scale, heal, and manage containerized applications efficiently.
