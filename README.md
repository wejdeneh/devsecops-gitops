
# DevSecOps GitOps Repository

## Overview

This repository contains the GitOps configuration used to deploy and manage the **Cloud Native DevSecOps Control Center** on Kubernetes using **ArgoCD** and **Helm**.

The application source code, container image build process, and security pipeline are maintained in a separate application repository. This repository is responsible for the deployment lifecycle and desired cluster state.

---

## Architecture

```text
Developer
    |
    v
GitHub Application Repository
    |
    v
GitHub Actions CI Pipeline
    |
    +--> Semgrep (SAST)
    +--> Gitleaks (Secrets Detection)
    +--> Trivy (Container Security)
    +--> OWASP ZAP (DAST)
    |
    v
Docker Hub Registry
    |
    v
GitOps Repository
    |
    v
ArgoCD
    |
    v
Helm Chart
    |
    v
Kubernetes Cluster
    |
    +--> Deployment
    +--> Service
    +--> Pods
    +--> Monitoring
````

---

## Purpose

This repository demonstrates modern GitOps practices by treating Kubernetes manifests and Helm charts as the single source of truth for application deployment.

Any change committed to this repository is automatically detected and synchronized by ArgoCD, ensuring that the Kubernetes cluster always matches the desired state stored in Git.

---

## Technology Stack

### GitOps & Deployment

* GitHub
* ArgoCD
* Helm
* Kubernetes

### Application Runtime

* Python
* Flask
* Docker

### DevSecOps Security Pipeline

* Semgrep
* Gitleaks
* Trivy
* OWASP ZAP

### Observability

* Prometheus
* Grafana

---

## Repository Structure

```text
.
├── devsecops-demo/
│   ├── Chart.yaml
│   ├── values.yaml
│   └── templates/
│       ├── deployment.yaml
│       ├── service.yaml
│       ├── servicemonitor.yaml
│       └── ...
│
└── README.md
```

---

## Helm Deployment

The application is packaged as a Helm chart.

### Features

* Configurable replica count
* Resource requests and limits
* Health probes
* Security context
* NodePort service
* Prometheus monitoring integration

Example values:

```yaml
replicaCount: 2

image:
  repository: wejdenehm/devsecops-demo
  tag: latest

service:
  type: NodePort
  port: 80
  targetPort: 5000
```

---

## Kubernetes Security

The deployment follows container security best practices.

### Pod Security Context

```yaml
securityContext:
  runAsNonRoot: true
  runAsUser: 1000
  fsGroup: 1000
```

### Container Security Context

```yaml
securityContext:
  allowPrivilegeEscalation: false

  capabilities:
    drop:
      - ALL
```

### Health Checks

Readiness Probe

```yaml
httpGet:
  path: /health
  port: 5000
```

Liveness Probe

```yaml
httpGet:
  path: /health
  port: 5000
```

---

## ArgoCD GitOps Workflow

ArgoCD continuously monitors this repository and automatically synchronizes changes to the Kubernetes cluster.

Workflow:

```text
Git Commit
    |
    v
GitOps Repository
    |
    v
ArgoCD Detects Change
    |
    v
Helm Rendering
    |
    v
Kubernetes Synchronization
    |
    v
Updated Application
```

### Benefits

* Declarative infrastructure
* Version-controlled deployments
* Automated synchronization
* Rollback capability
* Reduced configuration drift

---

## Monitoring

The platform exposes Prometheus metrics through the application.

Prometheus collects metrics from:

```text
/metrics
```

Visualization is provided through Grafana dashboards.

Monitoring components:

* Prometheus
* Grafana
* ServiceMonitor
* Application Metrics

---

## Related Repositories

### Application Repository

Contains:

* Flask application
* Dockerfile
* GitHub Actions pipeline
* Security scanning configuration

Repository:

```text
https://github.com/wejdeneh/devsecops-demo-app
```

### GitOps Repository

Contains:

* Helm charts
* Kubernetes manifests
* ArgoCD deployment configuration
* Monitoring resources

---

## Key DevSecOps Capabilities Demonstrated

* GitOps Continuous Delivery
* Kubernetes Deployments
* Helm Package Management
* Infrastructure as Code
* Secure Container Deployment
* Automated Security Validation
* Continuous Synchronization with ArgoCD
* Health Monitoring
* Observability with Prometheus and Grafana

---

## Author

**Wejden Haj Mefteh**

Cloud Engineering Student | Certified Kubernetes Administrator (CKA)

Focused on Cloud Native Platforms, Kubernetes Security, GitOps, Platform Engineering, and DevSecOps Automation.

```
```
