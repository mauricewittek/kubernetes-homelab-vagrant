## Based on
https://www.itwonderlab.com/en/ansible-kubernetes-vagrant-tutorial/

## Prerequisites
- A Linux workstation with at least 16 GB of RAM and 15 GB of free hard disk space for the virtual machines.
- Vagrant 2.2.16
    ```bash
    wget https://releases.hashicorp.com/vagrant/2.2.16/vagrant_2.2.16_x86_64.deb
    sudo apt install ./vagrant_2.2.16_x86_64.deb
    ```
- VirtualBox 6.1.22 or above
    ```bash
    sudo apt install virtualbox
    ```
- Ansible 2.9.9
    ```bash
    sudo apt-add-repository --yes --update ppa:ansible/ansible
    sudo apt install ansible
    ```

## Deploying the cluster

```bash
vagrant up
```

## Check the cluster

```bash
# access cluster
vagrant ssh k8s-master-1

# check nodes:
kubectl get nodes

# check running pods:
kubectl get pods -A
```

## Copy kube config

```bash
# Create the configuration directory
mkdir -p ~/.kube

# Find the SSH port of the k8s-m-1 server
vagrant port k8s-master-1

# Copy the file using scp (ssh password is vagrant)
scp -P 2222 vagrant@127.0.0.1:/home/vagrant/.kube/config ~/.kube/config
```

## Useful vagrant commands

```bash
# Create the cluster or start the cluster after a host reboot
vagrant up

# Execute the Ansible playlist on all vagrant vms, useful during development of Ansible playbooks
vagrant provision 

#Execute the Ansible playlist one a single node
vagrant provision k8s-worker-1

# Poweroff the Kubernetes Cluster
vagrant halt

# Open an ssh connection to a node
vagrant ssh k8s-master-1
```