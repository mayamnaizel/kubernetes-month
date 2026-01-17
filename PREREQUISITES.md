# Prerequisites – Kubernetes Observability Lab

This document describes the required setup for running all labs locally.

It is intentionally minimal and workshop‑friendly.

---

## Supported Operating Systems

* Ubuntu: 20.04 LTS, 22.04 LTS, 24.04 LTS
* macOS: Intel & Apple Silicon (M1/M2/M3)

---

## What You Will Install

By the end of this guide, you will have:

* Docker (container runtime)
* kubectl (Kubernetes CLI)
* Minikube (local Kubernetes cluster)
* Helm (Kubernetes package manager)

These are the only prerequisites required for the lab.

---

# Ubuntu Setup

## 1. Update the System

```bash
sudo apt update && sudo apt upgrade -y
```

---

## 2. Install Base Packages

```bash
sudo apt install -y \
  ca-certificates \
  curl \
  gnupg \
  lsb-release \
  apt-transport-https
```

---

## 3. Install Docker

### Add Docker GPG key

```bash
sudo mkdir -p /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | \
  sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
```

### Add Docker repository

```bash
echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] \
https://download.docker.com/linux/ubuntu \
$(lsb_release -cs) stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

### Install Docker

```bash
sudo apt update
sudo apt install -y docker-ce docker-ce-cli containerd.io
```

### Enable Docker and add user permissions

```bash
sudo systemctl enable docker
sudo systemctl start docker
sudo usermod -aG docker $USER
```

Log out and log back in before continuing.

Verify:

```bash
docker ps
```

---

## 4. Install kubectl

```bash
curl -LO "https://dl.k8s.io/release/$(curl -Ls https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
chmod +x kubectl
sudo mv kubectl /usr/local/bin/
```

Verify:

```bash
kubectl version --client
```

---

## 5. Install Minikube

```bash
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
sudo install minikube-linux-amd64 /usr/local/bin/minikube
```

Verify:

```bash
minikube version
```

---

## 6. Start Minikube (Docker Driver)

```bash
minikube start --driver=docker
```

Verify:

```bash
kubectl get nodes
```

---

## 7. Install Helm

```bash
curl https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3 | bash
```

Verify:

```bash
helm version
```

---

# macOS Setup

## 1. Install Homebrew (if not installed)

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

Verify:

```bash
brew --version
```

---

## 2. Install Docker Desktop

Install Docker Desktop from:

[https://www.docker.com/products/docker-desktop/](https://www.docker.com/products/docker-desktop/)

After installation:

* Open Docker Desktop
* Wait until it shows **Docker is running**

Verify:

```bash
docker ps
```

---

## 3. Install kubectl

```bash
brew install kubectl
```

Verify:

```bash
kubectl version --client
```

---

## 4. Install Minikube

```bash
brew install minikube
```

Verify:

```bash
minikube version
```

---

## 5. Start Minikube (Docker Driver)

```bash
minikube start --driver=docker
```

Verify:

```bash
kubectl get nodes
```

---

## 6. Install Helm

```bash
brew install helm
```

Verify:

```bash
helm version
```

---

# Final Verification (All OS)

Run all of the following:

```bash
docker ps
kubectl get nodes
helm version
minikube status
```

If all commands succeed, your system is **ready for the lab**.

---

## Notes for Workshops

* Use Docker + Minikube only 
* Start Docker before Minikube
* If something breaks, restart Docker first

---

## Next Step

Proceed to:

Week 2 Lab – Kubernetes Networking

Week 3 Lab – Kubernetes Observability with Prometheus & Grafana
