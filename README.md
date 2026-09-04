# ☸️ Kubernetes Core Concepts & Workloads Portfolio

An end-to-end repository showcasing declarative Kubernetes orchestration, core workload management, and multi-tenancy isolation. Built as part of a professional DevOps engineering workflow utilizing imperative generation techniques for rapid manifest deployment and CKA-standard efficiency.

# 🗺️ Portfolio Architecture & Sub-Projects

### k8s-portfolio

**core-concepts/:**  Foundational Kubernetes API workloads directory.

**core-concepts/namespace.yaml:**  Multi-tenancy environment isolation definition (dev-environment).

**core-concepts/pod.yaml:** Standalone atomic workload manifest running Nginx (pod1).

**core-concepts/deployment.yaml:** Declarative, scalable deployment controller running Nginx with 3 replicas (deploy1).

# 🛠️ Core Concepts & Methodologies Implemented

**Imperative Dry-Run Generation:** Utilizing `kubectl --dry-run=client -o yaml` to instantly construct production-grade YAML skeletons, drastically reducing syntax errors and deployment setup time.

**Multi-Tenancy Isolation:** Defining explicit Namespace scopes (`dev-environment`) to isolate workloads and prevent cross-environment namespace pollution.

**Atomic Workloads vs. Declarative Controllers:** Understanding the fundamental behavior differences between ephemeral Pod instances (`pod1`) and self-healing Deployment controllers (`deploy1`).

**Declarative Scaling & Self-Healing:** Enforcing high availability by maintaining 3 active application replicas across the cluster with dynamic state reconciliation.

# 📂 Featured Workloads Breakdown

## 1️⃣ 01-core-concepts — Fundamental API Objects
**Description:** A foundational module demonstrating the lifecycle of Kubernetes core components. Focuses on imperative dry-run generation for high speed and declarative manifest accuracy.
Path: ./core-concepts/
Key Files: namespace.yaml, pod.yaml, deployment.yaml

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
