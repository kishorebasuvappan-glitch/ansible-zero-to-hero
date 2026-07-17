# Day 1: Ansible Fundamentals and Environment Setup

## 1. Core Concepts

### What is Ansible?
Ansible is an open-source IT automation engine used for configuration management, application deployment, infrastructure provisioning, and orchestration.

### Agentless Architecture
Unlike traditional automation tools, Ansible does not require agents running on target machines. It connects over standard protocols:

- SSH for Linux/Unix systems
- WinRM or SSH for Windows systems

### Idempotency
Idempotency is one of Ansible's core principles. Running the same playbook multiple times always results in the desired system state without performing unnecessary changes.

Example:

- A package that is already installed will not be installed again.
- A service that is already running will not be restarted unless required.

### Declarative Automation
Ansible uses human-readable YAML files where you describe the desired state instead of writing procedural scripts.

---

# 2. Lab Environment

The lab consists of one control node managing two Ubuntu virtual machines.

## Control Node

- Ansible installed
- Executes playbooks and ad-hoc commands

## Managed Nodes

| Host | Purpose | OS |
|------|---------|----|
| 192.168.1.50 | Web Server 01 | Ubuntu |
| 192.168.1.51 | Web Server 02 | Ubuntu |

---

# 3. Installation and Configuration

## Step 3.1 — Install Ansible

Update the package index and install Ansible on the control node.

```bash
# Update package index
sudo apt update

# Install required packages
sudo apt install software-properties-common -y

# Add the official Ansible repository
sudo apt-add-repository --yes --update ppa:ansible/ansible

# Install Ansible
sudo apt install ansible -y

# Verify installation
ansible --version
```

---

## Step 3.2 — Configure Passwordless SSH

Generate an SSH key and copy it to each managed node.

```bash
# Generate an ED25519 SSH key
ssh-keygen -t ed25519 -C "ansible-control-key" -f ~/.ssh/id_ed25519 -N ""

# Copy the public key to Web Server 01
ssh-copy-id -i ~/.ssh/id_ed25519 ubuntu@192.168.1.50

# Copy the public key to Web Server 02
ssh-copy-id -i ~/.ssh/id_ed25519 ubuntu@192.168.1.51

# Verify SSH connectivity
ssh -i ~/.ssh/id_ed25519 ubuntu@192.168.1.50 "echo 'SSH Connection Successful'"
```

---

## Step 3.3 — Create the Inventory File

Create a file named `hosts.ini`.

```ini
[webservers]
192.168.1.50
192.168.1.51

[all:vars]
ansible_user=ubuntu
ansible_ssh_private_key_file=~/.ssh/id_ed25519
```

The inventory file defines:

- Target hosts
- Host groups
- Connection variables

---

# 4. Verify Connectivity

Run the built-in `ping` module against every host.

```bash
ansible all -m ping -i hosts.ini
```

Expected output:

```json
192.168.1.50 | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python3"
    },
    "changed": false,
    "ping": "pong"
}

192.168.1.51 | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python3"
    },
    "changed": false,
    "ping": "pong"
}
```

> **Note**
>
> The Ansible `ping` module is **not** an ICMP network ping.
>
> It verifies that Ansible can:
>
> - Authenticate using SSH
> - Execute Python on the remote machine
> - Return a JSON response successfully

---

# 5. Troubleshooting

## YAML and INI Formatting

- Use spaces instead of tabs.
- Maintain proper indentation.
- Verify syntax before execution.

---

## Python Requirement

Managed nodes must have Python installed.

If Python is missing, install it using:

```bash
ansible all -m raw -a "sudo apt update && sudo apt install -y python3"
```

---

## Host Key Verification

If SSH host verification causes connection errors, create an `ansible.cfg` file in the project directory.

```ini
[defaults]
host_key_checking = False
```

---

# Summary

By the end of this lab, you should have:

- Installed Ansible
- Configured passwordless SSH authentication
- Created an inventory file
- Verified connectivity using the Ansible `ping` module
- Learned common troubleshooting techniques
