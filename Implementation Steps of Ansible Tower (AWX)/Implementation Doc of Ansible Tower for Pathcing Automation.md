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

**After this you have to add the credentials on AWX (Ansible Tower) UI.**
### Step 2).To Add the Inventory on AWX:
Go to AWX ⇒ Resources ⇒ Inventories ⇒ click on Add Inventory.
Under Inventory fill the below fields.
- **Name**: Windows-Linux_Server
- **Description**: 
- **Organization**: Default
- click on **Save**.
  
After create **Inventory** just click on that Inventory name: **windows-Linux_Server**
Under this above Inventory 
Go to **Hosts**

Under the Hosts you can add the host details of each server.

**Eg: Name: Linux_Server** 
```bash
Add this host details in variables:
ansible_host: 172.31.3.199  (Linux server private ip)
ansible_connection: ssh
ansible_python_interpreter: /usr/bin/python3
```

**Eg: Name: Win_Server.**
 Add this host details in **variable:**
 ```bash
ansible_host: 172.31.13.30  (Windows server private ip)
ansible_connection: winrm
ansible_port: 5985
ansible_winrm_transport: ntlm
ansible_winrm_server_cert_validation: ignore
```

### Step 3).After adding the Host details into the Inventory section. Now we need to add the worker Node credentials to AWX(Ansible Tower).
Go to AWX ⇒ Resources ⇒ Credentials ⇒ Click on Add
After clicking on Add you have to fill the below fields.

**Name:** 
**Description**:
**Organization**: You can add your own created Organization or you can go with Default also.
**Credential Type**: Machine
**Username**: Enter the user name here eg: ubuntu
**Password**: 
Or **SSH Private key**:  
**Privilege Escalation Method**: sudo ( only for Linux machine you can added here )
**Note**: when you add linux machine credentials then you can use SSH Private key and when you use Windows machine then you can go with Password



