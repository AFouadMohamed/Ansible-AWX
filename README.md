# Ansible-AWX

![image](https://github.com/user-attachments/assets/2a7d2202-07f3-4b94-ac76-f44f0122e428)

Ansible AWX is a free and open-source front-end web application that provides a user interface to manage Ansible playbooks and inventories, as well as a REST API for Ansible. It is an open-source version of Red Hat Ansible Tower.
In this post, we will show you how to install Ansible AWX on Ubuntu 22.04 or Ubuntu 20.04. To deploy AWX, some Kubernetes Infrastructure needs to be installed, such as MicroK8s, K3s, or Minikube. In this demo, we will use minikube ( A Single node Kubernetes cluster).

# Prerequisites


Before we get started, ensure that the Ubuntu 22.04 or 20.04 system has the following:

- 4 GB of RAM
- 3.4 GHz CPU with 2 Cores
- Hard disk space 20 GB
- Internet Connection
- Pre Installed minikube

# Step 1: Install Required Packages
$ sudo apt install git make -y

# Step 2: Start minikube cluster

$ minikube start --vm-driver=docker --addons=ingress

![image](https://github.com/user-attachments/assets/4a0d9c6e-e9e2-4660-ada1-bd69daa30bf3)

$ minikube status

$ kubectl get pods -A

![image](https://github.com/user-attachments/assets/c20682a7-bff8-43c2-8941-cefd26a23da2)


# Step 3: Deploy Ansible AWX via Operator

