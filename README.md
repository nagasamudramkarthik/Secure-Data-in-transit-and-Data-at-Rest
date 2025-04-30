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
![cryptsetup](https://img.shields.io/badge/cryptsetup-efefef?style=for-the-badge&logo=linux&logoColor=black&labelColor=gray)
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
 3.  **LUKS encryption**
      Follow the below steps for the luks encryption
      1. **Create a 1GB file-backed virtual disk**
       ```
         dd if=/dev/zero of=luks-image.img bs=1M count=1024
       ```
      2. **Encrypt the file with LUKS (you’ll be prompted for a passphrase)**
      ```
        sudo cryptsetup luksFormat /encrypted-disk.img

       ```
      3. **Open it and create a mapping called "backend-data"**
      ```
       sudo cryptsetup luksOpen /encrypted-disk.img backend-disk

       ```
      4. **Format with ext4**
       ```
       sudo mkfs.ext4 /dev/mapper/backend-disk
       ```
       5. **Close the LUKS Encrypted Device**  
        After unmounting the device, securely close the LUKS-encrypted 
       device: 
       ```
         sudo cryptsetup close backend-disk
        ```
       6. **Mount the Virtual Disk**  
        Mount the encrypted device to `/dev/loop12`:  
        ```bash
        sudo losetup /dev/loop12 /path/to/your/encrypted_file
        ```
        Make sure that LUKS passphrase key is securely stored in hashiCorp vault.
  4.  **HashiCorp Vault setup**
      Refer to the official HashiCorp Vault Kubernetes Minikube tutorial to deploy a Vault instance within your Minikube cluster and makesure to install it in a namespace 
     called dencrypt

  5. **Project setup**
     1. **first create namespace in which we run the whole project**
     ```
     kubectl create namespace dencrypt
     ```
     2. **Apply the peer-authentication.yaml and destination-rule.yaml to the namespace for ensuring data-in-transit encryption  using istio**
        You can apply yaml files to namespace using the below command
        ```
        kubectl apply -f <filename>.yaml -n <namespace>
        ```
     3. **Apply the frontend.yaml, backend.yaml, pv.yaml, pvc.yaml"
         To view the pods that are running in a namespace enter the below command
        ```
        kubectl get pods -n dencrypt
        ```
     4. **Apply webapp.yaml file"
          this webapp is a pod that fetches the key from vault when ever a request is made to it and also make sure vault-0 is running in the namespace. backend pod will make request to  fetch key while decrypting the disk
     5. "Execute frontend pod"
         You can execute the frontend pod using the below command
        ```
          kubectl exec -it <frontend-pod-name> -n dencrypt -- sh
        ```
        in the bash script of the pod make a request to backendpod
        ```
           $ curl http://backend:5678
        ```
        this is will execute the backend and it write data to the decrypted disk
         
     
    
     
