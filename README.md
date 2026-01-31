# 🧩 MostoxDB | MicroK8s IaC – NGINX and MongoDB

This repository contains an **Infrastructure as Code (IaC)** project for the progressive deployment of a containerized architecture using **Kubernetes (MicroK8s)**.  
The architecture itself it's (in it`s basic form) just a Nginx + MongoDB deployment.

---

## 📚 Index

- [📖 Project explanation](#-project-explanation)
- [⚙️ Environment setup](#️-environment-setup)
- [🚀 Deployment](#-deployment)
  - [Version 1 – NGINX + MongoDB (no backend)](#version-1--nginx--mongodb-no-backend)
  - [Version 2 – NGINX + Backend + MongoDB](#version-2--nginx--backend--mongodb)
  - [Version 3 – Under development](#version-3--under-development)
- [✅ Deployment verification](#-deployment-verification)

---

## 📖 Project explanation

The goal of this project is to demonstrate the use of **Kubernetes as a container orchestration platform**, applying the **Infrastructure as Code** approach through YAML manifests (for education purposses).

The architecture is deployed incrementally:

1. **V1 'basic-deploy'**: Basic deployment of NGINX and MongoDB as independent services.
2. **V2 'functional-system'**: Introduction of a backend API responsible for handling communication between NGINX and MongoDB.
3. **V3 'systemist-aproach'**: Future evolution (to be defined).

Each version is being developed in a **separate Git branch** using them as diferent "levels" of depth.

---

## ⚙️ Environment setup

### Requirements

- Linux system (or virtual machine)
- MicroK8s installed
- Git

### MicroK8s installation

```bash
sudo snap install microk8s --classic
```

Add your user to the MicroK8s group:

```bash
sudo usermod -a -G microk8s $USER
```

Check cluster status:

```bash
microk8s status --wait-ready
```

Enable DNS (recommended):

```bash
microk8s enable dns
```

---

## 🚀 Deployment

Each deployment version is located in a **dedicated branch** of this repository.

---

### Version 1 – NGINX + MongoDB (no backend)

**Branch:** `main`

#### Description

Basic deployment including:
- One NGINX pod
- One MongoDB pod
- Internal Services for connectivity
- NGINX exposed using a NodePort Service

⚠️ In this version, **no functional communication** exists between NGINX and MongoDB.

#### Deployment steps

```bash
git checkout main
microk8s kubectl apply -f deploy.yaml
```

---

### Version 2 – NGINX + Backend + MongoDB

**Branch:** `functional-system`

#### Description

Complete architecture including:
- NGINX as HTTP server and reverse proxy
- Backend API (Node.js) handling application logic
- MongoDB as the persistence layer
- Service-to-service communication using Kubernetes internal DNS

NGINX forwards requests on `/api` to the backend, which connects to MongoDB.

#### Deployment steps

```bash
git checkout functional-system
microk8s kubectl apply -f deploy.yaml
```

---

### Version 3 – Under development

**Branch:** `systemist-aproach`

#### Status

🚧 Under development.

Planned improvements:
- Bash script to manage the deploy
- Secrets management
- Log system

---

## ✅ Deployment verification

### Check created resources

```bash
microk8s kubectl get pods
microk8s kubectl get svc
```

### Access NGINX

From a browser or terminal:

```
http://HOST_IP:30080
```

### API verification (version 2)

```
http://HOST_IP:30080/api
```

Expected response:

```
API connected successfully to MongoDB
```

---

## 🧠 Final notes

- Kubernetes does **not manage startup dependencies**, only the desired state.
- Inter-service communication is implemented at the application level.
- The entire environment is reproducible using YAML manifests (IaC).

---

✍️ Project developed by mosto for educational purposes (ASIR / Kubernetes training).

