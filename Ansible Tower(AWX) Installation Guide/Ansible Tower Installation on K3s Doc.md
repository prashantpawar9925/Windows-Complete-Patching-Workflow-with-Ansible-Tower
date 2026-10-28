# **Ansible Tower (AWX Operator) Installation on K3s Documentation.**
**K3s**: K3s is a light-weight kubernetes distribution. K3s is developed by Rancher Labs. It can be used as a single node in a cluster.

## Prerequisites:
- 4vCPU
- 8GB RAM

## Follow below provided steps ##
### Step 1.To Update Your System
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

### Step 2.Install k3s
*(AWX Operator requires Kubernetes. For your single-node AWS lab, K3s is a convenient lightweight Kubernetes distribution. )*
- curl -sfL https://get.k3s.io | sh - 

**To check K3s status:**
- sudo systemctl status k3s
- sudo systemctl is-active k3s

### Step 3.Configure kubectl
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


### Step 5.Create AWX Namespace 
- kubectl create namespace awx

**To verify:**
- kubectl get namespace awx

### Step 6.Create AWX Kustomization Directory
- mkdir -p ~/awx-deployment cd ~/awx-deployment 

**To Verify:** 
- pwd

### Step 7: Create `kustomization.yaml`

Create the `kustomization.yaml` file:

```bash
vim kustomization.yaml
```

Add the following configuration:

```yaml
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
```
**Verify Kustomization:**
- kubectl kustomize .
  
(This should generate Kubernetes manifests. If you get YAML/output instead of an error, the Kustomization is valid.)


### Step 8.Apply the configuration:

```bash
kubectl apply -k .
```
### Step 9.Verify Operator is Running
- kubectl get pods -n awx

### Step 10.Create AWX Instance. Create a file named `awx-demo.yaml`

```bash
vim awx-demo.yaml
```
```yaml
apiVersion: awx.ansible.com/v1beta1
kind: AWX
metadata:
  name: awx-demo
  namespace: awx
spec:
  service_type: NodePort
  nodeport_port: 32000
```
### Step 11.Add Instance to Kustomization
 Update your kustomization.yaml to include `awx-demo.yaml`

```bash
vim kustomization.yaml
```
#add - `awx-demo.yaml` under resources

```yaml
apiVersion: kustomize.config.k8s.io/v1beta1
kind: Kustomization
namespace: awx

resources:
  - github.com/ansible/awx-operator/config/default?ref=2.19.1
  - awx-demo.yaml

images:
  - name: quay.io/ansible/awx-operator
    newTag: 2.19.1

  - name: gcr.io/kubebuilder/kube-rbac-proxy:v0.15.0
    newName: registry.k8s.io/kubebuilder/kube-rbac-proxy
    newTag: v0.15.0
```

### Step 12.Reapply Kustomize Configuration
```bash
kubectl apply -k .
```

### Step 13. Check POD Status
- kubectl get awx -n awx 
- kubectl get pods -n awx    or 
- kubectl get pods -n awx -w 
- kubectl get all -n awx

**To Check Operator Deployment** 
- kubectl get deployment -n awx
- kubectl get deployment awx-operator-controller-manager -n awx
- kubectl get pods -n awx -o wide 

### Step 14. View Logs
- kubectl logs -f deployment/awx-operator-controller-manager -c awx-manager -n awx

**To check Services:**
- kubectl get svc -n awx 

### Step 15. Get the AWX admin password 
First check the secret: 
- kubectl get secrets -n awx 
Then, if the secret is `awx-demo-admin-password:`

**Retrieve Admin Password**
- kubectl get secret awx-demo-admin-password -n awx -o jsonpath="{.data.password}" | base64 --decode 
 
### Step 16. Access the AWX Dashboard
- http://<your-server-ip>:32000
 
 #Username: admin
 #Password: (from previous step)

