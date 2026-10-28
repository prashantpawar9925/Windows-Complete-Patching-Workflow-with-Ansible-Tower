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
