Automated Linux and Windows Server Patching Using Ansible AWX / Tower

Project Overview

This project automates operating system patching for Linux and Windows servers using Ansible Tower / AWX, with centralized orchestration and standardized patch management.

The workflow performs pre-patching health checks, creates AWS EBS snapshots before patch installation, installs approved operating system updates, handles reboots when required, and validates server health after patching. It also generates patch compliance reports to provide operational visibility and an auditable record of patching activities.

The solution is designed for Linux and Windows virtual machines hosted on AWS EC2 and can be adapted to other supported environments.

Project Objectives

Reduce manual patching effort through automation.

Standardize patch management across Linux and Windows servers.

Create AWS EBS snapshots before operating system changes to support recovery.

Install approved patches through controlled Ansible workflows.

Minimize downtime by rebooting servers only when required.

Validate server health and patch installation after updates.

Generate auditable patch compliance reports.

Improve repeatability, operational visibility, and consistency across patching operations.

Key Features

Centralized orchestration: Manage patching jobs through AWX / Ansible Tower.

Pre-patching health checks: Validate server connectivity, operating system details, available disk space, and other required conditions.

Automated backup: Create EBS snapshots of the relevant EC2 volumes before patch installation.

Controlled patch installation: Apply approved Linux and Windows operating system updates.

Reboot management: Restart servers only when required and wait for them to become available.

Post-patching validation: Verify patch installation, server connectivity, and system health.

Compliance reporting: Record patch status, server details, reboot results, and validation outcomes.

Workflow-based execution: Separate job templates into stages and connect them using AWX Workflow Job Templates.
