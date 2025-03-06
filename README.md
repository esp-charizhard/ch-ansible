# ch-ansible
Configuration for the charizhard infrastructure

## Structure 

### k8s-prep.yml
Playbook to bootstrap k8s cluster

4 roles :
-  **spawn-k8s**: On every node of the cluster, to install dependencies, set network rules, install cri (containerd)...
- **spawn-control-panel**: Only the master nodes (for now it's just a control-plane), use of kubeadm and set cni (flannel)
- **spawn-worker-node**: Only on the worker nodes, to perform the kubeadm join
- **spawn-nginx**: On the control-plane, to perform a small hello-world app

It has a clean script if the *spawn-control-panel* and *spawn-worker-node*

### clean.yml

Playbook to clean the actions performed on every node in case it hasn't cleaned in case of error, or if you need to relaunch the *k8s-prep.yml* playbook
## Install requirements

1. Install Python
2. Install Ansible [See tutorial](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html)
3. Clone the repo
4. Create Python environnement

## Roadmap

- [ ] Test architecture (1 master / 1 worker)
    - [x] Install all dependencies on nodes
    - [x] Set up control plane
    - [x] Set up worker node
    - [x] Set up small app
    - [x] Expose app
    - [ ] Set up Ingress service
    - [x] Get OTA microservice deployment
    - [ ] Set up Keycloak deployment
    - [ ] Set up database for replicas pods
- [ ] Change in HA architecture
    - [ ] External etcd ?
    - [ ] Increase master nodes to 3
    - [ ] Increase worker nodes to 3
- [ ] Set up Grafana/Prometheus
