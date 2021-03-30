# Kubernetes Step by Step 
URL: ```https://phoenixnap.com/kb/install-kubernetes-on-ubuntu```

```
sudo apt-get update
```

## Install Docker
```
sudo apt-get install docker.io
```

## Confirm Docker
```
docker ––version
```
## Step 2 - Start and Enable Docker
### Set Docker to launch at boot by entering the following:
```
sudo systemctl enable docker
```
Verify Docker is running
```
sudo systemctl status docker
```
Start Docker
```
sudo systemctl start docker
```

# Install Kubernetes
## Add Kubernetes Signing Key
Since you are downloading Kubernetes from a non-standard repository, it is essential to ensure that the software is authentic. This is done by adding a signing key.
```
curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add
```
```
sudo apt-get install curl
```


## Add Software Repositories
```
sudo apt-add-repository "deb http://apt.kubernetes.io/ kubernetes-xenial main"
```
` These steps above should be repeated for all the nodes to be added to the cluster `

## Kubernetes Installation Tools
Kubeadm (Kubernetes Admin) is a tool that helps initialize a cluster. It fast-tracks setup by using community-sourced best practices. Kubelet is the work package, which runs on every node and starts containers. The tool gives you command-line access to clusters

Install Kubernetes tools with the command:

```
sudo apt-get install kubeadm kubelet kubectl

sudo apt-mark hold kubeadm kubelet kubectl
```
verify the installation
```
kubeadm version
```
` These steps above should be repeated for all the nodes to be added to the cluster `

## Kubernetes Deployment
### Step 6: Begin Kubernetes Deployment
Start by disabling the swap memory on each server:

```
sudo swapoff –a
```
## Assign Unique Hostname for Each Server Node 
` Decide which server to set as the master node. Then enter the command: `
```
sudo hostnamectl set-hostname master-node
```
` Next, set a worker node hostname by entering the following on the worker server: `
```
sudo hostnamectl set-hostname worker01
```

` If you have additional worker nodes, use this process to set a unique hostname on each. `

#  Initialize Kubernetes on Master Node
## Switch to the master server node, and enter the following:

```
sudo kubeadm init --pod-network-cidr=10.244.0.0/16
```
` Once this command finishes, it will display a kubeadm join message at the end. Make a note of the whole entry. This will be used to join the worker nodes to the cluster. `

Next, enter the following to create a directory for the cluster

```
kubernetes-master:~$ mkdir -p $HOME/.kube

kubernetes-master:~$ sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config

kubernetes-master:~$ sudo chown $(id -u):$(id -g) $HOME/.kube/config
```

## Deploy Pod Network to Cluster
A Pod Network is a way to allow communication between different nodes in the cluster. This tutorial uses the flannel virtual network.

Enter the following:
```
sudo kubectl apply -f https://raw.githubusercontent.com/coreos/flannel/master/Documentation/kube-flannel.yml
```
Allow the process to complete.

`Verify that everything is running and communicating:`
```
kubectl get pods --all-namespaces
```

# Join Worker Node to Cluster
As indicated in Step 7, you can enter the kubeadm join command on each worker node to connect it to the cluster.

Switch to the worker01 system and enter the command you noted
```
kubeadm join --discovery-token abcdef.1234567890abcdef --discovery-token-ca-cert-hash sha256:1234..cdef 1.2.3.4:6443
```
` Replace the alphanumeric codes with those from your master server. Repeat for each worker node on the cluster. Wait a few minutes; then you can check the status of the nodes. `
Switch to the master server, and enter:
```
kubectl get nodes
```
`The system should display the worker nodes that you joined to the cluster.`