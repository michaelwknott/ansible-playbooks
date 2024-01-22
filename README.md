# ansible-playbooks
A repository of Ansible playbooks for various tasks

## Table of Contents
- [Getting Started](#getting-started)
  - [Prerequisites](#prerequisites)
  - [Installation](#installation)
- [Playbooks](#playbooks)
  - [Server Setup and Security](#server-setup-and-security)

## Getting Started

### Prerequisites
- [Python 3.11](https://www.python.org/)
- [Ansible 9](https://docs.ansible.com/)
- [Pre-commit](https://pre-commit.com/) (optional)

### Installation

1. Clone the repo
    ```
    git clone git@github.com:michaelwknott/ansible-playbooks.git
    ```

1. Create a virtual environment
   ```
   python -m venv .venv --prompt .
   ```

1. Activate your virtual environment
   ```
   .venv/bin/activate
   ```
1. Ansible. I installed Ansible to be globally available using Pipx. See the following [Ansible documentation](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html#installing-and-upgrading-ansible-with-pipx) for more information. Alternatively you can add Ansible to the `requirements.txt` file.

1. Install requirements
   ```
   python -m pip install requirements.txt
   ```
1. Install pre-commit hooks
   ```
   pre-commit install
   ```

## Playbooks

### Server Setup and Security

This playbook is designed to secure and harden a server's security. It performs the following tasks:
 - Updates the system packages
 - Installs unattended-upgrades and configures it to automatically install security updates
 - Updates SSH configuration to disable root login and password authentication
 - Adds a local user with sudo privileges and allows user to run sudo commands without a password
 - Adds a ssh directory for the local user and copies the public key to the authorized_keys file
 - Installs and configures ufw to only allow SSH on IPv4 from a specific IP address
 - Installs fail2ban

To use this playbook, you will need to create a inventory and vars file with the following contents:

```ini
# inventory.ini
# Update the values to match your server:
# - host: The IP address of your server
[host]
<ip address>
```

```yaml
# vars.yaml
# Update the values to match your server:
# - username: The username of the local user to create
# - trusted_ip: The IP address that will be allowed to SSH into the server
# - ssh_public_key_path: The path to your SSH public key
# - ssh_port: The port that SSH is running on

username: <your_username_here>
trusted_ip: <your_ip_address_here>
ssh_public_key_path: <your_ssh_public_key_path_here>
ssh_port: <your_ssh_port_here>
```

To run the playbook, use the following command in your terminal:

```bash
ansible-playbook -i inventory.ini server-setup-and-security.yaml
```
