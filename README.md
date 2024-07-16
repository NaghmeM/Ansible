Thank you for providing the inventory file. I'll update the README to include this information. Here's the expanded README:

# Ansible Learning Project

## Project Overview
This repository documents my journey in learning Ansible, an open-source automation tool. As a self-learner, I'm using this project to understand and apply Ansible concepts for infrastructure automation and configuration management.

## Project Structure
The project currently includes:

1. Ansible configuration file (`ansible.cfg`)
2. Ansible playbook for system updates and web server setup
3. Inventory file

## Key Components

### Ansible Configuration (`ansible.cfg`)
```ini
[default]
inventory = inventory
private_key_file = ~/.ssh/ansible
```

This configuration file sets up the following defaults:
- The inventory file is named `inventory` and is expected to be in the same directory as the `ansible.cfg` file.
- The private SSH key for connecting to managed nodes is located at `~/.ssh/ansible`.

### Ansible Playbook
```yaml
---
- hosts: all
  become: true
  tasks:
  - name: install updates (Ubuntu)
    apt:
      upgrade: dist
      update_cache: yes
    when: ansible_distribution_version == "Ubuntu"

- hosts: web_servers
  become: true
  tasks:
  - name: install apache and php for Ubuntu servers
    apt:
      name:
        - apache2
        - libapache2-mod-php
      state: latest
    when: ansible_distribution == "Ubuntu"
```

This playbook does the following:
1. Updates all Ubuntu systems in the inventory.
2. Installs Apache web server and PHP on hosts in the `web_servers` group, but only for Ubuntu distributions.

### Inventory File
```ini
[web_servers]
192.168.51.247
192.168.51.248

[file_servers]
192.168.51.249
```

This inventory file defines two groups of servers:
- `web_servers`: Contains two servers (192.168.51.247 and 192.168.51.248)
- `file_servers`: Contains one server (192.168.51.249)

## Learning Objectives
- Understanding Ansible configuration basics
- Managing inventory in Ansible
- Secure connection to managed nodes using SSH keys
- Writing and structuring Ansible playbooks
- Using conditionals in Ansible tasks
- Managing system updates with Ansible
- Installing and configuring web servers
- Organizing hosts into groups for targeted automation

## Usage
1. Ensure you have Ansible installed on your control node.
2. Place the `ansible.cfg` file in your project's root directory.
3. Create the `inventory` file in the same directory with the provided content.
4. Ensure you have the appropriate SSH key at `~/.ssh/ansible`.
5. Create a playbook file (e.g., `site.yml`) with the provided playbook content.
6. Run the playbook using the command:
   ```
   ansible-playbook site.yml
   ```

## Next Steps
- Expand the playbook to include tasks for `file_servers`
- Implement role-based access control for different server groups
- Explore Ansible modules for file management and other server configurations
- Learn about Ansible roles for better organization of tasks
- Implement error handling and logging in playbooks
- Explore Ansible Vault for managing sensitive data

## Challenges and Learnings
- Understanding the structure of Ansible playbooks
- Learning to use conditionals to target specific distributions
- Figuring out how to manage different tasks for different host groups
- Organizing and managing inventory for different server roles

## Resources
- [Ansible Documentation](https://docs.ansible.com/)
- [Ansible Configuration File](https://docs.ansible.com/ansible/latest/reference_appendices/config.html)
- [Ansible Playbook Best Practices](https://docs.ansible.com/ansible/latest/user_guide/playbooks_best_practices.html)
- [Ansible Inventory](https://docs.ansible.com/ansible/latest/user_guide/intro_inventory.html)

## Note
This is a learning project and may not reflect best practices for production environments. Always refer to official documentation and security best practices when working on real-world projects.
