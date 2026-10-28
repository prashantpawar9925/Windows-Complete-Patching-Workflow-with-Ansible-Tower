# **Ansible Tower (AWX Operator) Installation on K3s Documentation.**
**K3s**: K3s is a light-weight kubernetes distribution. K3s is developed by Rancher Labs. It can be used as a single node in a cluster.

## Prerequisites:
- 4vCPU
- 8GB RAM
  
**1.To Update Your System**
sudo apt-get update 
sudo apt-get upgrade -y

**Install required utilities:** 
sudo apt install -y \
    curl \
    wget \
    git \
    vim \
    jq \
    unzip \
    ca-certificates

**To Verify:**
git - - version
curl - - version
