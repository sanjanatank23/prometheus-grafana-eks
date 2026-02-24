
# 🚀 End-to-End Monitoring, Alerting & GitOps Foundation (EKS)

## 📌 Project Overview

This project demonstrates a **complete end-to-end DevOps workflow** covering:

- Monitoring with **Prometheus**
- Visualization and alerting with **Grafana**
- **Real email alerting** using **Gmail SMTP**
- Alert testing and tuning
- Understanding of **SMTP internals**
- Foundation for **GitOps deployment using ArgoCD**
- Migration mindset from **CI-based deployment → GitOps**

All work was implemented practically and validated step by step.

---

## 🧱 Architecture Overview

```

Node Exporter → Prometheus → Grafana → Gmail SMTP → Email Inbox
|
↓
Alert Rules

Git (Manifests Repo)
↓
ArgoCD
↓
EKS (Mario App)

```

---

## 🛠️ Tools & Technologies Used

- Docker & Docker Compose
- Prometheus
- Node Exporter
- Grafana
- Gmail SMTP (App Password)
- Kubernetes (EKS – existing cluster)
- Git & GitHub
- GitOps concepts
- ArgoCD (GitOps engine – next phase)

---

## 📂 Project Structure

```

prometheus-grafana/
├── docker-compose.yml
├── prometheus.yml
└── README.md

```

---

## 🚀 Step 1: Monitoring Stack Setup

The monitoring stack was deployed locally using **Docker Compose**:

- **Prometheus** for metrics collection
- **Node Exporter** for system-level metrics
- **Grafana** for dashboards and alerting

Grafana was configured with a **persistent volume** to ensure dashboards and alerts are not lost on container restart.

---

## 📊 Step 2: Grafana Configuration

- Logged into local Grafana UI
- Added Prometheus as a data source
- Used Docker internal DNS:

```

[http://prometheus:9090](http://prometheus:9090)

```

---

## 📈 Step 3: Dashboard Creation

Custom dashboards were manually created using PromQL:

- CPU Usage %
- Memory Usage %
- Disk Usage
- Network Traffic
- System Load
- Node Exporter health

Dashboards were organized using rows for clean layout.

---

## 🚨 Step 4: Alert Configuration (New Grafana Alerting)

A CPU usage alert was created using **new Grafana alerting** (not legacy panel alerts).

### Alert Configuration

- Metric: CPU Usage
- Query:
```

100 - (avg by (instance)(rate(node_cpu_seconds_total{mode="idle"}[5m])) * 100)

```
- Condition: CPU > 80%
- Pending Period: 1 minute
- Evaluation Interval: 1 minute
- Labels:
- severity=warning
- service=monitoring
- Folder: System Alerts

Alert lifecycle verified:
```

Normal → Pending → Firing

```

---

## 📧 Step 5: Real Email Alerting Using Gmail SMTP

### Why SMTP?

Grafana cannot send emails on its own.  
An **SMTP server** is required to deliver alert notifications.

---

### Gmail SMTP Setup

- Enabled **2-Step Verification** on Gmail account
- Generated **Gmail App Password**
- Configured SMTP in Grafana using environment variables

### SMTP Configuration Used

```

SMTP Server: smtp.gmail.com
Port: 587
Authentication: App Password
Encryption: STARTTLS

````

---

### Result

- CPU alert triggered successfully
- **Real email alert received in Gmail inbox**
- End-to-end monitoring and alerting validated


## 🧠 SMTP Knowledge Gained

### What is an SMTP Server?

An SMTP server is responsible for **sending emails**.
Grafana uses an external SMTP server (Gmail) to send alert notifications.

---

### Why Port 587?

* Standard port for **authenticated SMTP submission**
* Supports STARTTLS encryption
* Recommended for applications

---

### SMTP Handshake (Simplified)

1. Client connects to SMTP server
2. EHLO exchange
3. STARTTLS encryption
4. Authentication (App Password)
5. MAIL FROM / RCPT TO
6. Email queued and delivered

---

### SMTP Server vs SMTP Relay

| SMTP Server            | SMTP Relay            |
| ---------------------- | --------------------- |
| Stores inboxes         | Does not store emails |
| Manages users          | Forwards emails only  |
| Used by mail providers | Used by applications  |

Gmail SMTP and AWS SES are **SMTP relays**.

---

## 🔄 GitOps & ArgoCD (Conceptual + Practical Foundation)

### What is GitOps?

GitOps is a deployment methodology where:

* **Git is the single source of truth**
* Kubernetes state must always match Git
* Changes are made via Git, not kubectl

---

### What is ArgoCD?

ArgoCD is a **GitOps tool** that:

* Runs inside Kubernetes
* Watches a Git repository
* Syncs Kubernetes resources automatically
* Self-heals drift

## 🔄 CI-Based Deployment vs GitOps

### Before (CI-Based)

```
CI
 ├─ Build image
 ├─ Push image
 └─ kubectl apply ❌
```

### After (GitOps)

```
CI
 ├─ Build image
 ├─ Push image
 └─ Update image tag in Git

ArgoCD
 └─ Syncs Git → EKS automatically
```


