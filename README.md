# ch-ansible
Configuration for the charizhard infrastructure

## Structure 

### k8s-prep.yml
Playbook to bootstrap k8s cluster

4 roles :
-  **spawn-k8s**: On every node of the cluster, to install dependencies, set network rules, install cri (containerd)...
- **spawn-control-panel**: Only the master nodes (for now it's just a control-plane), use of kubeadm and set cni (calico)
- **spawn-worker-node**: Only on the worker nodes, to perform the kubeadm join
- **spawn-ota**: On the control-plane, to deploy the ota, minio object storage and keycloak

It has a clean script if the *spawn-control-panel* and *spawn-worker-node*

To launch this playbook, use this command :

```
ansible-playbook k8s-prep.yml --vault-password-file vault_pass.txt
```
### ota-launch.yml
Playbook to deploy all microservices

1 role :
- **spawn-ota**: On the control-plane, to deploy the ota, minio object storage and keycloak

To launch this playbook, use this command :

```
ansible-playbook ota-launch.yml --vault-password-file vault_pass.txt
```

### clean.yml

Playbook to clean the actions performed on every node in case it hasn't cleaned in case of error, or if you need to relaunch the *k8s-prep.yml* playbook

To launch this playbook, use this command :

```
ansible-playbook clean.yml --vault-password-file vault_pass.txt
```

## Install requirements

1. Install Python
2. Install Ansible [See tutorial](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html)
3. Clone the repo
4. Create Python environnement
5. Ask the super duper admin for the secret vault_pass.txt
6. copy you ssh-key on all the vms machine

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
    - [x] Set up database for replicas pods
- [x] Change in HA architecture
    - [x] External etcd ?
    - [x] Increase master nodes to 3
    - [x] Increase worker nodes to 3
- [ ] Set up Grafana/Prometheus
