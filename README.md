# 🔐 Secure Data at Rest and In Transit

## 📚 Table of Contents

1. [Project Overview](#project-overview)
2. [Tools Used](#tools-used)
3. [Requirements](#requirements)
4. [Steps to Run the Project](#steps-to-run-the-project)
5. [Web Application Code](#web-application-code)
6. [Understanding Deployments](#understanding-deployments)
    - [MongoDB Configuration](#mongodb-configuration)
    - [MongoDB Sealed Secrets](#mongodb-sealed-secrets)
    - [Mutual TLS (mTLS) Configuration](#mutual-tls-mtls-configuration)
    - [MongoDB Image and Persistent Volume](#mongodb-image-and-persistent-volume)
    - [Web Application](#web-application)

---

## 📝 Project Overview

This project showcases a secure Kubernetes-based setup where **data in transit** and **data at rest** are both protected. It involves two pods: a **frontend web application** and a **backend MongoDB database**. 

- **Istio** provides mutual TLS (mTLS) for encrypted communication between services.
- **MongoDB** stores sensitive data, which is protected using a **LUKS-encrypted persistent volume**.
- The LUKS decryption key is securely managed via **HashiCorp Vault**.
- **Sealed Secrets** are used to securely manage MongoDB credentials in Kubernetes.

---

## 🛠️ Tools Used

![Docker](https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white)
![Kubernetes](https://img.shields.io/badge/Kubernetes-326CE5?style=for-the-badge&logo=kubernetes&logoColor=white)
![Minikube](https://img.shields.io/badge/Minikube-F5C452?style=for-the-badge&logo=minikube&logoColor=black)
![Istio](https://img.shields.io/badge/Istio-466BB0?style=for-the-badge&logo=istio&logoColor=white)
![Vault](https://img.shields.io/badge/HashiCorp%20Vault-000000?style=for-the-badge&logo=vault&logoColor=white)
![HTML](https://img.shields.io/badge/HTML5-E34F26?style=for-the-badge&logo=html5&logoColor=white)
![CSS](https://img.shields.io/badge/CSS3-1572B6?style=for-the-badge&logo=css3&logoColor=white)
![Node.js](https://img.shields.io/badge/Node.js-339933?style=for-the-badge&logo=nodedotjs&logoColor=white)

---

## ⚙️ Requirements

To run this project, ensure your system meets the following:

- **Operating System**: Linux (Ubuntu recommended) with LUKS support.
- **Docker**: To build and run containers.
- **Kubernetes**: For managing deployments.
- **Minikube**: To set up a local Kubernetes cluster.
- **Istio CLI**: To configure service mesh and mTLS.
- **HashiCorp Vault**: For secure secret management.
- **Kubeseal**: To manage Sealed Secrets.

---

## 🚀 Steps to Run the Project

### 1. Clone the Repository

```bash
git clone https://github.com/pavansai444/secure-data-at-rest-and-secure-data-in-transit.git
cd secure-data-at-rest-and-secure-data-in-transit
