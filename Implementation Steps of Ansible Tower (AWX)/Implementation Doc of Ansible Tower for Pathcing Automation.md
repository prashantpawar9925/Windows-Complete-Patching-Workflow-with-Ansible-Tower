# **Implementation Steps of Ansible Tower (AWX) for Patching Automation:**
## To Added Worker Node (Win & Linux )  to AWX( Ansible Tower)
**ON LINUX SERVER**

**First you have to create key pair on AWX (Ansible Tower) Server**
```bash
ssh-keygen 
```
**Copy public key from AWX_Server to Worker Node (ubuntu_Server)**
**Copy public key to remote machine(worker node)**
```bash
cd ~./ssh
```
```bash
vim authorized_keys
```
**To copy key pair**
```bash
ssh-copy-id user_name@private_ip
```
**To give a permission**
```bash
chmod 700 ~/.ssh/authorized_keys
``` 
**To ssh login to worker node from AWX (Ansible Tower) Server**
```bash
ssh ubuntu@ip_of_worker_node.
```
## Below are the Provided Steps to perform on Ansible Tower/AWX UI.
### Step 1).To Create Organization: 
- Go to AWX ⇒ Access ⇒ Organization ⇒ click on Add .
- Enter the following details to create a new organization.
- **Name**: AWX_Organization
- **Description**: 
- **Galaxy Credentials**: keep it default 

