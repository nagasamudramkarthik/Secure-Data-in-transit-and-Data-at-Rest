# Secure Data at Rest and In Transit with Kubernetes, Istio, and Vault

## 📖 Project Overview

This repository demonstrates how to secure **data at rest** and **data in transit** in a Kubernetes environment. The project sets up secure communication between two pods: a **frontend pod** and a **backend pod**.

- **mTLS with Istio** is used to encrypt data in transit between the frontend and backend.
- **LUKS-encrypted Persistent Volumes** secure data at rest in the backend pod.
- **HashiCorp Vault** securely stores and delivers the decryption passphrase used to unlock the encrypted volume.

---

## 🛠️ Tools Used

- **Docker** – Containerization of the application.
- **Kubernetes** – Container orchestration platform.
- **Minikube** – Local Kubernetes cluster for development.
- **Istio** – Service mesh for securing service-to-service traffic using mTLS.
- **HashiCorp Vault** – Secret management for storing and retrieving the LUKS passphrase.
- **Linux with LUKS** – Native support for encrypting persistent volumes.

---

## 📋 Requirements

Ensure your Linux-based development environment (preferably Ubuntu) includes the following:

- [Docker](https://docs.docker.com/get-docker/)
- [Kubernetes](https://kubernetes.io/docs/setup/)
- [Minikube](https://minikube.sigs.k8s.io/docs/start/)
- [Istio CLI](https://istio.io/latest/docs/setup/getting-started/)
- [HashiCorp Vault](https://developer.hashicorp.com/vault/docs/install)
- LUKS encryption support via `cryptsetup`

---

## 🚀 Steps to Run the Project

### 1. Clone the Repository

```bash
git clone https://github.com/nagasamudramkarthik/Secure-Data-in-transit-and-Data-at-Rest.git
cd Secure-Data-in-transit-and-Data-at-Rest
