# 🚀 Ansible Playbook Masterclass

![Ansible](https://img.shields.io/badge/Ansible-Automation-red?logo=ansible)
![YAML](https://img.shields.io/badge/YAML-Configuration-blue)
![DevOps](https://img.shields.io/badge/DevOps-Infrastructure-orange)
![License](https://img.shields.io/badge/License-MIT-green)

A beginner-friendly guide to **Ansible Playbooks** covering playbook syntax, modules, inventory, execution, best practices, and DevOps automation.

---

# 📑 Table of Contents

- Introduction
- Architecture
- Folder Structure
- Playbook Keywords
- Playbook Anatomy
- Common Modules
- Inventory
- Running Playbooks
- Check Mode
- ansible-pull
- Playbook Validation
- Best Practices
- Common Errors
- Git Commands
- Resources

---

# 📖 Introduction

Ansible is an **agentless IT automation tool** used for:

- Configuration Management
- Application Deployment
- Infrastructure as Code (IaC)
- Server Provisioning
- Cloud Automation

It communicates with remote machines using:

- SSH (Linux)
- WinRM (Windows)

---

# 🏗 Architecture

```
                   +----------------------+
                   |   Control Node       |
                   | (Ansible Installed)  |
                   +----------+-----------+
                              |
             -----------------+-----------------
            SSH                              SSH
              |                                |
     +--------+--------+              +--------+--------+
     | Managed Node 1  |              | Managed Node 2  |
     |  Web Server     |              | Database Server |
     +-----------------+              +-----------------+
```

---

# 📂 Project Structure

```
ansible-project/
│
├── inventory/
│   └── hosts.ini
│
├── playbooks/
│   └── nginx.yml
│
├── templates/
│   └── index.html.j2
│
├── files/
│
├── vars/
│   └── variables.yml
│
└── README.md
```

---

# 🔑 Playbook Keywords

| Keyword | Description |
|----------|-------------|
| hosts | Target machines |
| name | Play/Task description |
| gather_facts | Collect system information |
| become | Use sudo privileges |
| become_user | Target user |
| become_method | Privilege escalation method |
| vars | Variables |
| vars_files | External variable files |
| tasks | Tasks to execute |
| handlers | Triggered tasks |
| notify | Calls handlers |
| tags | Run selected tasks |

---

# 📝 Sample Playbook

```yaml
---
- name: Install and Configure Nginx
  hosts: webservers
  become: true
  gather_facts: true

  vars:
    http_port: 80
    doc_root: /var/www/html

  tasks:

    - name: Install Nginx
      apt:
        name: nginx
        state: present

    - name: Copy Web Page
      template:
        src: index.html.j2
        dest: "{{ doc_root }}/index.html"

      notify:
        - Restart Nginx

  handlers:

    - name: Restart Nginx
      service:
        name: nginx
        state: restarted
```

---

# 📦 Common Modules

| Module | Purpose |
|----------|----------|
| apt | Install packages |
| yum | Package management |
| service | Manage services |
| systemd | Linux services |
| copy | Copy files |
| template | Jinja2 templates |
| file | Manage files |
| lineinfile | Edit configuration |
| shell | Execute shell commands |
| command | Execute commands |

---

# 📁 Inventory File

```ini
[webservers]
192.168.1.10
192.168.1.11

[database]
192.168.1.20
```

---

# ▶ Running Playbooks

## Normal Execution

```bash
ansible-playbook -i inventory/hosts.ini playbooks/nginx.yml
```

---

## Syntax Check

```bash
ansible-playbook \
-i inventory/hosts.ini \
playbooks/nginx.yml \
--syntax-check
```

---

## Dry Run (Check Mode)

```bash
ansible-playbook \
-i inventory/hosts.ini \
playbooks/nginx.yml \
--check
```

---

## Verbose Output

```bash
ansible-playbook playbook.yml -vvv
```

---

## Parallel Execution

```bash
ansible-playbook playbook.yml -f 10
```

---

# 🔄 Ansible Pull

Instead of pushing configurations:

```
Control Node
      ↓
Managed Nodes

```

Use **ansible-pull** where each server pulls configurations from Git.

```bash
ansible-pull \
-U https://github.com/username/repository.git
```

Ideal for:

- Cloud
- Auto Scaling
- Kubernetes Nodes

---

# ✅ Validate Playbooks

## Check Syntax

```bash
ansible-playbook playbook.yml --syntax-check
```

## List Tasks

```bash
ansible-playbook playbook.yml --list-tasks
```

## List Hosts

```bash
ansible-playbook playbook.yml --list-hosts
```

## Show Differences

```bash
ansible-playbook playbook.yml --diff
```

---

# 🔍 Linting

```bash
ansible-lint playbook.yml
```

Example Output

```text
[403] Package installs should not use latest

Task: Install Apache
```

---

# 🎨 Execution Colors

| Color | Meaning |
|--------|---------|
| 🟢 Green | No changes required |
| 🟡 Yellow | Configuration changed |
| 🔴 Red | Task failed |

---

# 💡 Best Practices

- ✅ Always use `name`
- ✅ Prefer modules over shell
- ✅ Use handlers for restarts
- ✅ Store secrets in Ansible Vault
- ✅ Keep variables in `vars/`
- ✅ Use templates for configs
- ✅ Use tags for selective execution
- ✅ Follow idempotent design

---

# ❌ Common Mistakes

❌ Wrong indentation

```yaml
tasks:
 - name:
```

✔ Correct

```yaml
tasks:
  - name:
```

---

❌ Using shell unnecessarily

```yaml
shell: apt install nginx
```

✔ Better

```yaml
apt:
  name: nginx
  state: present
```

---

# 📚 Useful Commands

```bash
ansible all -m ping

ansible --version

ansible-playbook site.yml

ansible-playbook site.yml --check

ansible-playbook site.yml --syntax-check

ansible-playbook site.yml --list-hosts

ansible-playbook site.yml --list-tasks
```

---

# 🚀 Git Commands

```bash
git init

git add README.md

git commit -m "Add Ansible Playbook Guide"

git branch -M main

git remote add origin https://github.com/<username>/<repo>.git

git push -u origin main
```

---

# 📖 Resources

- Official Ansible Documentation
- Ansible Galaxy
- Jinja2 Documentation
- YAML Specification

---

# ⭐ Support

If this repository helped you:

⭐ Star the repository

🍴 Fork it

🛠 Contribute improvements

---

# 📜 License

This project is licensed under the MIT License.

---

## Happy Automating! 🚀
