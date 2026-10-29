## **Automated Linux and Windows Server Patching Using Ansible AWX / Tower**

## **Project Overview**

This project automates operating system patching for Linux and Windows servers using Ansible Tower / AWX, with centralized orchestration and standardized patch management.

The workflow performs pre-patching health checks, creates AWS EBS snapshots before patch installation, installs approved operating system updates, handles reboots when required, and validates server health after patching. It also generates patch compliance reports to provide operational visibility and an auditable record of patching activities.

The solution is designed for Linux and Windows virtual machines hosted on AWS EC2 and can be adapted to other supported environments.

## **Project Objectives**

- Reduce manual patching effort through automation.

- Standardize patch management across Linux and Windows servers.

- Create AWS EBS snapshots before operating system changes to support recovery.

- Install approved patches through controlled Ansible workflows.

- Minimize downtime by rebooting servers only when required.

- Validate server health and patch installation after updates.

- Generate auditable patch compliance reports.

- Improve repeatability, operational visibility, and consistency across patching operations.

## **Key Features**

**1.Centralized orchestration**: Manage patching jobs through AWX / Ansible Tower.

**2.Pre-patching health checks**: Validate server connectivity, operating system details, available disk space, and other required conditions.

**3.Automated backup**: Create EBS snapshots of the relevant EC2 volumes before patch installation.

**4.Controlled patch installation**: Apply approved Linux and Windows operating system updates.

**5.Reboot management**: Restart servers only when required and wait for them to become available.

**6.Post-patching validation**: Verify patch installation, server connectivity, and system health.

**7.Compliance reporting**: Record patch status, server details, reboot results, and validation outcomes.

**8.Workflow-based execution**: Separate job templates into stages and connect them using AWX Workflow Job Templates.

## **Patching Workflow**

The patching process follows these stages:

**Pre-check**: Validate connectivity, operating system details, disk space, and system readiness.

**Snapshot creation**: Create AWS EBS snapshots of the relevant volumes before patching.

**Snapshot verification**: Confirm that the required snapshots have been created successfully.

**Patch installation**: Install approved operating system updates on Linux and Windows servers.

**Reboot handling**: Restart the server when required by the update process.

**Post-check**: Verify server availability, operating system health, and patch installation.

**Compliance reporting**: Generate a report showing patching results and compliance status.

## **Architecture Diagram**:

![Architecture Diagram](https://github.com/user-attachments/assets/d080155f-2045-4ef1-bd9a-1fc144ba6f6d)

## **Ansible Tower(AWX) Installation Guide**

[Installation Guide](https://github.com/prashantpawar9925/Windows-Complete-Patching-Workflow-with-Ansible-Tower/tree/main/Ansible%20Tower%28AWX%29%20Installation%20Guide)

## **Implementation Steps of Ansible Tower (AWX)**

[Implementation Guide](https://github.com/prashantpawar9925/Windows-Complete-Patching-Workflow-with-Ansible-Tower/tree/main/Implementation%20Steps%20of%20Ansible%20Tower%20(AWX))
