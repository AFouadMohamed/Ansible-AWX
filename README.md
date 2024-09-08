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
$ git clone https://github.com/ansible/awx-operator.git

$ cd awx-operator/

$ git checkout 2.4.0

![image](https://github.com/user-attachments/assets/10983048-2c3f-43d5-99ba-14fb698741d8)

$ export NAMESPACE=ansible-awx

$ make deploy

![image](https://github.com/user-attachments/assets/274cef86-7321-47c3-8249-eda24cde4827)

$ kubectl get pods -n ansible-awx

![image](https://github.com/user-attachments/assets/8a2983ed-abd4-47fc-a1d1-f73a92949a5c)

# Step 4: Deploy AWX 
$ cat awx-demo.yml

$ kubectl create -f awx-demo.yml -n ansible-awx

![image](https://github.com/user-attachments/assets/11a2e885-cdb5-48c2-b70a-f02f7b11c127)

$ kubectl get pods -n ansible-awx

$ kubectl get svc -n ansible-awx

![image](https://github.com/user-attachments/assets/3121a6b9-fb34-4e50-b2cf-9c31913aabe4)

# Step 5: Access AWX Dashboard

$ minikube service awx-demo-service --url -n ansible-awx
http://192.168.49.2:30182                                                   -----------------> minikube ip

$ kubectl port-forward service/awx-demo-service -n ansible-awx --address 0.0.0.0 10445:80

![image](https://github.com/user-attachments/assets/45461c74-0c27-4fbf-a9df-95df2a32f791)

$ http://<Ubuntu-System-IP-Address>:10445          --------------> open browser

$ ![image](https://github.com/user-attachments/assets/d1582164-ff8e-4749-81c1-db16dc40c73f)

$ kubectl get secret awx-demo-admin-password -o jsonpath="{.data.password}" -n ansible-awx | base64 --decode; echo
7EliSIHKyM28KLQQcZ2zBzdKWGlnz6JM

# Can Use Lens to get secret

![Screenshot from 2024-09-08 16-48-25](https://github.com/user-attachments/assets/75ddba91-24e9-4a9e-924f-379482dab889)

![image](https://github.com/user-attachments/assets/842ba541-cb14-4ac9-89dc-88a773fbd69c)

![image](https://github.com/user-attachments/assets/20c09c9b-bde8-4a47-9303-c148d317c997)

![image](https://github.com/user-attachments/assets/847f3a3f-322c-4ddb-a947-5f02ba721bac)











