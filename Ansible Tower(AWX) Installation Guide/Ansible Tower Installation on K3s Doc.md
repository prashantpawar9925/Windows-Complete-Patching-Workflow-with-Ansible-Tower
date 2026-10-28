# **Ansible Tower (AWX Operator) Installation on K3s Documentation.**
**K3s**: K3s is a light-weight kubernetes distribution. K3s is developed by Rancher Labs. It can be used as a single node in a cluster.

## Prerequisites:
- 4vCPU
- 8GB RAM

## Follow below provided steps ##
**Step 1.To Update Your System**
- sudo apt-get update 
- sudo apt-get upgrade -y

**Install required utilities:** 
- sudo apt install -y \
    curl \
    wget \
    git \
    vim \
    jq \
    unzip \
    ca-certificates

**To Verify:**
- git - - version
- curl - - version

**Step 2.Install k3s**
*(AWX Operator requires Kubernetes. For your single-node AWS lab, K3s is a convenient lightweight Kubernetes distribution. )*
- curl -sfL https://get.k3s.io | sh - 

**To check K3s status:**
- sudo systemctl status k3s
- sudo systemctl is-active k3s

**Step 3.Configure kubectl**
 ( K3s creates its kubeconfig at:  /etc/rancher/k3s/k3s.yaml )

**Instead of changing ownership of the K3s-managed file, copy it to your user's .kube directory:**
- mkdir -p ~/.kube
- sudo cp /etc/rancher/k3s/k3s.yaml ~/.kube/config

**Set ownership:** 
- sudo chown $USER:$USER ~/.kube/config
  
**Set the environment variable:** 
- export KUBECONFIG=~/.kube/config
  
**To make it persistent:** 
- echo 'export KUBECONFIG=~/.kube/config' >> ~/.bashrc
  
**Reload:** 
- source ~/.bashrc

4.Verify Kubernetes Cluster
kubectl version
kubectl get nodes
kubectl get pods -A (To check all pods)
Kubectl cluster-info


**Step 5.Create AWX Namespace** 
- kubectl create namespace awx

**To verify:**
- kubectl get namespace awx

**Step 6.Create AWX Kustomization Directory**
- mkdir -p ~/awx-deployment cd ~/awx-deployment 

**To Verify:** 
- pwd

**Step 7.Create kustomization.yaml**
*vim kustomization.yaml*

apiVersion: kustomize.config.k8s.io/v1beta1
kind: Kustomization
namespace: awx

resources:
  - github.com/ansible/awx-operator/config/default?ref=2.19.1

images:
  - name: quay.io/ansible/awx-operator
    newTag: 2.19.1

  - name: gcr.io/kubebuilder/kube-rbac-proxy:v0.15.0
    newName: registry.k8s.io/kubebuilder/kube-rbac-proxy
    newTag: v0.15.0

