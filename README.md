# ☸️ Kubernetes Core Concepts & Workloads Portfolio

An end-to-end repository showcasing declarative Kubernetes orchestration, core workload management, and multi-tenancy isolation. Built as part of a professional DevOps engineering workflow utilizing imperative generation techniques for rapid manifest deployment and CKA-standard efficiency.

# 🗺️ Portfolio Architecture & Sub-Projects

### k8s-portfolio

* **core-concepts/:**  Foundational Kubernetes API workloads directory.
  * **core-concepts/namespace.yaml:**  Multi-tenancy environment isolation definition (dev-environment).
  * **core-concepts/pod.yaml:** Standalone atomic workload manifest running Nginx (pod1).
  * **core-concepts/deployment.yaml:** Declarative, scalable deployment controller running Nginx with 3 replicas (deploy1).

* **taints-tolerations/:** Advanced pod scheduling and node repulsion mechanisms.
  * **pod-toleration.yml:** Pod configured with matching tolerations for dedicated node placement.
  * **deploy-toleration.yml:** Deployment template passing tolerations to underlying replica pods.

* **services/:** Service discovery and cluster networking manifests.
  * **ClusterIP.yaml:** Internal cluster communication endpoint.
  * **NodePort.yaml:** External access point exposing node ports (30080).
  * **LoadBalancer.yaml:** Cloud-integrated dynamic external load balancer.

* **rollouts-updates/:** Zero-downtime deployment strategies and lifecycle management.
  * **Rollingupdate.yaml:** Zero-downtime deployment strategy (maxSurge: 25%, maxUnavailable: 0).
  * **Recreate.yaml:** Complete workload replacement strategy for breaking changes.

# 🛠️ Core Concepts & Methodologies Implemented
* **Imperative Dry-Run Generation:** Utilizing `kubectl --dry-run=client -o yaml` to instantly construct production-grade YAML skeletons, drastically reducing syntax errors and deployment setup time.

* **Multi-Tenancy Isolation:** Defining explicit Namespace scopes (`dev-environment`) to isolate workloads and prevent cross-environment namespace pollution.

* **Atomic Workloads vs. Declarative Controllers:** Understanding the fundamental behavior differences between ephemeral Pod instances (`pod1`) and self-healing Deployment controllers (`deploy1`).

* **Declarative Scaling & Self-Healing:** Enforcing high availability by maintaining 3 active application replicas across the cluster with dynamic state reconciliation.

* **Node Repulsion & Workload Placement:** Applying Taints to nodes and matching Tolerations to pods/deployments to enforce dedicated infrastructure allocation.
  
* **Service Discovery & Cluster Networking:** Exposing internal pod sets using stable virtual IPs (ClusterIP), node-level ports (NodePort), and external cloud balancers (LoadBalancer).
 
* **Zero-Downtime Application Lifecycle:** Executing production rollout strategies using RollingUpdate for seamless releases and Recreate for maintenance windows.

--- 

# 📂 Featured Workloads Breakdown

## 1️⃣ core-concepts — Fundamental API Objects
**Description:** A foundational module demonstrating the lifecycle of Kubernetes core components. Focuses on imperative dry-run generation for high speed and declarative manifest accuracy.
Path: ./core-concepts/
Key Files: *namespace.yaml*, *pod.yaml*, *deployment.yaml*

## 2️⃣ taints-tolerations — Pod Scheduling & Isolation
*Description:* Demonstrates how nodes use Taints (NoSchedule) to repel pods unless explicitly permitted via Tolerations.
* *Path:* ./taints-tolerations/
* *Key Components:*
  * Node Tainting: **kubectl taint nodes <node-name> app=prod:NoSchedule**
  * Pod Toleration Matching: operator: **"Equal", key: "app", value: "prod", effect: "NoSchedule"**

## 3️⃣ services — Cluster Networking & Load Balancing
**Description:** Connects internal pod workloads to external traffic and internal microservices using Kubernetes networking abstractions.
* **Path:** ./services/
 ### Service Types:
  * ***ClusterIP:*** Default internal-only IP for inter-service communication.
  * ***NodePort:*** Exposes high-range ports (30000-32767) across all cluster worker nodes.
  * ***LoadBalancer:*** Provisions external cloud provider load balancers.

## 4️⃣ rollouts-updates — Deployment Lifecycle & Rollback Strategies
**Description:** Implements application upgrade controls, release tracking, and rollback capabilities.
* **Path:** ./rollouts-updates/
  ### Strategies Implemented:
  * **RollingUpdate:** Configured with (maxSurge: 25%) and (maxUnavailable: 0) for 100% operational availability during updates.
  * **Recreate:** Terminates all active pods simultaneously before starting new versions.


# 🚀 Quick Start Guide

## Prerequisites:
* Kubernetes Cluster active (Minikube, Kind, or Killercoda environment)
* kubectl CLI tool installed and configured

## Deploy Workloads
```bash
1. Provision Namespace Environment:
kubectl apply -f core-concepts/namespace.yaml

2. Deploy Core Workloads:
kubectl apply -f core-concepts/ -n dev-environment

3. Verify Cluster State:
kubectl get all -n dev-environment
    
4.Rollout & Update
  #Trigger Rolling Update
  kubectl set image deployment/deploy1 nginx-container=nginx:1.25 -n dev-environment
  # Monitor Rollout history
  kubectl rollout history deployment/deploy1 -n dev-environment
  # Undo / Rollback Deployment
  kubectl rollout undo deployment/deploy1 -n dev-environment

5. Services
  # without a yaml file
    kubectl expose deployment <deploy-name> --port <port-num> --target-port <port-num> --type ClusterIP
    kubectl expose deployment <deploy-name> --port <port-num> --port <port-num> --type NodePort
    kubectl expose deployment <deploy-name> --port <port-num> --target-port <port-num> --type LoadBalancer
