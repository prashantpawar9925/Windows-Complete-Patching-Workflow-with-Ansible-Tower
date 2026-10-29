# **Implementation Steps of Ansible Tower (AWX) for Patching Automation:**
## To Added Worker Node (Win & Linux ) to AWX( Ansible Tower)
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
## Below are the Provided Steps to Perform on Ansible Tower/AWX UI.
### Step 1).To Create Organization: 
- Go to **AWX ⇒ Access ⇒ Organization ⇒ click on Add** .
- Enter the following details to create a new organization.
- **Name**: AWX_Organization
- **Description**: 
- **Galaxy Credentials**: keep it default 

After this you have to add the credentials on **AWX (Ansible Tower)** UI.
### Step 2).To Add the Inventory on AWX:
Go to **AWX ⇒ Resources ⇒ Inventories ⇒ click on Add Inventory**.
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

Add this host details in **variables**:
```bash
ansible_host: 172.31.3.199  #(Linux server private ip)
ansible_connection: ssh
ansible_python_interpreter: /usr/bin/python3
```
![Linux_Server Host](https://github.com/user-attachments/assets/0d9ac2fc-e5be-44b0-b376-a75dbda5ab71)

**Eg: Name: Win_Server.**

 Add this host details in **variable:**
 ```bash
ansible_host: 172.31.13.30  #(Windows server private ip)
ansible_connection: winrm
ansible_port: 5985
ansible_winrm_transport: ntlm
ansible_winrm_server_cert_validation: ignore
```

### Step 3).After adding the Host details into the Inventory section. Now we need to add the worker Node credentials to AWX(Ansible Tower).
Go to **AWX ⇒ Resources ⇒ Credentials ⇒ Click on Add**

After clicking on Add you have to fill the below fields.

- **Name**:

- **Description**:

- **Organization**: You can add your own created Organization or you can go with Default also.

- **Credential Type**: Machine

- **Username**: Enter the user name here eg: ubuntu

- **Password**: 

- Or **SSH Private key**:  

- **Privilege Escalation Method**: sudo ( only for Linux machine you can added here )

- ## Note : when you add linux machine credentials then you can use SSH Private key and when you use Windows machine then you can go with Password

### Step 4).How to add the Project into AWX(Ansible Tower)
Go to **AWX ⇒ Projects ⇒ click on Add** (to create new project)

After clicking Enter the required fields below
- **Name**:
- **Description**:
- **Organization**:
- **Source Control Type**: Git 
- **Source control URL**: Enter the Git url here. (which is where your Ansible Playbook is stored.)
- Click on **Save**.
- After Save then you have to click on **Sync**.

![Synch](https://github.com/user-attachments/assets/f83f1198-ee1e-45ef-992b-a7ca088643eb)

*After adding the Project into the AWX(Ansible Tower)* , 

### Step 5).To create a Job template to run the Job.
**Job Template**:
*(A configuration for running an individual Ansible playbook against a selected inventory, using credentials and other execution settings.)
Example: Run the Linux pre-check playbook.* 

Go to **AWX ⇒ Resources ⇒ Templates ⇒ Click on Add job template**.(to create New job template)

After clicking Enter the Required fields below:

- **Name**:

- **Description**:

- **Job Type**: Run (keep default)

- **Inventory** : Select inventory here

- **Project**: Select project here

- **Playbook**: Select the playbook which you want to apply.

- **Credentials**: Select the Credentials here

- Click on **Save**.

- After Save just click on **Launch**.

![Launch](https://github.com/user-attachments/assets/1feb26cd-5b0d-402a-bd86-e0a98422b0f0)

### Step 6). To create a Workflow job template:
**Workflow Job Template**: 
*(A graphical workflow that connects multiple job templates, allowing you to control execution order and define what happens when a job succeeds or fails.)*
**Example**: Pre-check → Snapshot → Patch → Reboot → Compliance report.

Go to **AWX ⇒ Resources ⇒ Templates ⇒ Click on Add Workflow template**

After clicking Enter the required fields:

- **Name**:
  
- **Description**:

- **Organization**:
  
- **Inventory**: Select inventory here
  
- Click on **Save**.
  
After clicking on **Save**. you will get the prompt to click on Start to add the Nodes.

![Prompt](https://github.com/user-attachments/assets/3edc1e48-544f-4929-9480-85c38ab82ebb)

After clicking on **Start**

![start](https://github.com/user-attachments/assets/0e88b1f6-75cb-4c05-b2c4-646953d13c77)

Enter the following information fields:

- **Node Type** : Job Template (keep default)
  
- **Name**: here you have to select the Job template which you have already  created.
  
- Click on **Save**.

![save](https://github.com/user-attachments/assets/68662f4c-b6da-4f0a-adbf-0add9ab82caa)

After clicking on **Save** Option. you will get the **Visualizer** prompt

![visualizer](https://github.com/user-attachments/assets/1abd0627-1497-4667-93f6-e3463880ede7)

After this if we want to **add multiple Nodes (job template)** click on **Plus Icon ( + )** to add a **new node**.

![add multiple nodes](https://github.com/user-attachments/assets/d4a60828-bb84-41fb-8082-52e6a64fd4fc)

After clicking **+ Icon** to create a new node.

- Select On **Success**
  
- Click on **Next**

![Icon](https://github.com/user-attachments/assets/e4910eb6-ea44-422a-ad49-0c4f73d530bf)

After clicking on **Next** option. Again we have to add **nodes (job template)**

- **Node Type** : Job Template (keep default)
  
- **Name**: here you have to select the Job template which you have already  created.
  
- Click on **Save**.

![job template](https://github.com/user-attachments/assets/f7dc4d26-60fb-4db5-9fba-750a9e97a5fe)

After clicking on **Save** option you will get the same **visualizer prompt** it will add a **new node (job template)** in below SS.

![new node](https://github.com/user-attachments/assets/29941e51-2d2c-4493-9b43-fe9d91d23074)

Again if you want a **new node (job template)** to add. follow the same steps from above.
