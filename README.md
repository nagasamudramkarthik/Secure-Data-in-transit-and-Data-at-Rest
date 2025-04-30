# secure data at rest and secure data in transit

## Table of Contents

1. [Project Overview](#project-overview)
2. [Tools Used](#tools-used)
3. [Requirements](#requirements)
4. [Steps to Run the Project](#steps-to-run-the-project)

### Project Overview

This repository showcases how to secure both data at rest and data in transit within a Kubernetes environment. It implements secure communication between a frontend pod and a backend pod using mutual TLS (mTLS) provided by Istio. The backend pod, running MongoDB, uses a LUKS-encrypted persistent volume, which is automatically decrypted using a passphrase securely retrieved from HashiCorp Vault.

### Tools Used
![Docker](https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white)
![Minikube](https://img.shields.io/badge/Minikube-F5C452?style=for-the-badge&logo=minikube&logoColor=black)
![Kubernetes](https://img.shields.io/badge/Kubernetes-326CE5?style=for-the-badge&logo=kubernetes&logoColor=white)
![Istio](https://img.shields.io/badge/Istio-466BB0?style=for-the-badge&logo=istio&logoColor=white)
![HashiCorp Vault](https://img.shields.io/badge/HashiCorp%20Vault-000000?style=for-the-badge&logo=vault&logoColor=white)

### Requirements

To set up and run this project, make sure the following tools and platforms are installed on a Linux-based operating system (preferably Ubuntu):

- **Docker**: Used for containerizing and running application components.

- **Kubernetes**: Manages and orchestrates containerized workloads.

- **Minikube**:: Provides a local Kubernetes cluster for development and testing purposes.

- **Istio**: Secures and controls service-to-service communication via mTLS.

- **HashiCorp Vault**: Manages secrets and encryption keys securely.

- **LUKS support**: Your system(preferably Linux) must support LUKS (Linux Unified Key Setup) for encrypting persistent volumes

### Steps to Run the Project

Follow the below steps to run the project

1. **Clone the Repository**
    ```bash
    git clone https://github.com/pavansai444/secure-data-at-rest-and-secure-data-in-transit.git
    cd secure-data-at-rest-and-secure-data-in-transit
    ```
2. **Prerequisites are installed**
    Ensure all the required tools are installed [Requirements](#requirements) . start the minikube by running the below command
   ```
    Minikube start
   ```
 
