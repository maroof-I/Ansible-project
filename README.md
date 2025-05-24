# Ansible Automation Repository

This repository is a structured Ansible workspace designed to automate a variety of system administration tasks, including software installation, web server configuration, SSH environment setup, storage management, and connection profiling.

---

## Folder Structure Overview

This repository is organized into modular folders, each serving a specific purpose in automating system administration tasks using Ansible.

---

### `Ansible_Role/`
Contains reusable Ansible roles and a playbook to run them. This includes roles for tools like Git, NFS, and custom web server configurations, structured according to Ansible Galaxy standards.

---

### `Connection_Profiles/`
Defines and applies network configuration profiles to target machines. Useful for setting up or modifying interface settings in a consistent and automated way.

---

### `HTTPD_Status/`
Includes playbooks to install and manage the Apache HTTP server (`httpd`). Also contains templates and validation logic to ensure the server is properly configured and running.

---

### `Manage_Storage/`
Automates Linux storage management tasks such as creating partitions, setting up LVM (Logical Volume Management), configuring swap space, and cleaning up disk resources.

---

### `Setup_SSH/`
Prepares the environment for secure and automated Ansible communication via SSH. It includes configuration files and playbooks for initializing SSH keys and other connection prerequisites.


---

## Ansible_Role

### Description
This is the heart of the repository, using **Ansible roles** to modularize configuration management. It includes:

-  **geerlingguy.git** – Installs and configures Git.
-  **geerlingguy.nfs** – Sets up an NFS server with OS-specific configurations.
-  **web** – A custom role that deploys a basic web server with a templated index page.

### Key Files

- `ansible.cfg` – Configuration file that defines inventory and defaults.
- `inventory.ini` – Inventory of target hosts.
- `requirements.yml` – Lists external roles (e.g., from Ansible Galaxy).
- `web-role-playbook.yml` – Playbook to run the `web` role.

---

## Connection_Profiles

### Description
Defines and manages network profiles for system interfaces via the `network.yml` playbook.

---

##  HTTPD_Status

### Description
Contains playbooks for managing an Apache HTTP server.

### Key Playbooks

- `install-httpd.yml` – Installs Apache on target hosts.
- `httpd.conf.j2` – A Jinja2 template for HTTPD configuration.
- `block-play.yml` – Demonstrates block/rescue constructs.
- `check-requirements.yml` – Validates system preconditions.
- `vars.yml` – Stores variables used across the HTTPD playbooks.

---

##  Manage_Storage

### Description
Automates Linux storage management using LVM and partitions.

### Key Playbooks

- `create_parition.yml` – Creates disk partitions.
- `lvm.yml` – Configures logical volume management.
- `swap.yml` – Sets up swap space.
- `delete.yml` and `delete-lvm.yml` – Clean up partitions or LVM.

---

## Setup_SSH

### Description
Sets up a basic SSH configuration for Ansible control node access and environment prep.

### Files

- `ansible.cfg` – Local Ansible configuration for this context.
- `prepare-environment.yml` – Initializes SSH keys or environment setup for remote automation.

---

## How to Use

1. **Install required roles** (for Ansible_Role):
   ```bash
   ansible-galaxy install -r Ansible_Role/requirements.yml
   ```
2. **Run a playbook, for example:**
   ```bash
   cd Ansible_Role
   ansible-playbook web-role-playbook.yml -v
   ```
3. **Run storage or HTTPD-specific tasks:**
   ```bash
   ansible-playbook lvm.yml --check -v # you need to have ansible.cfg and inventory.ini
   ansible-playbook block-play.yml --check -v # you need to have ansible.cfg and inventory.ini
   ```

