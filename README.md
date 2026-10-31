# Automating Web Server Configuration on AWS EC2 Using Ansible

Automated installation, configuration, and deployment of an Nginx web server on an AWS EC2 Ubuntu instance using Ansible.

## Technology Stack

- AWS EC2
- Ubuntu Linux
- Ansible
- Nginx
- HTML/CSS
- Git and GitHub

## Implementation

### 1. Launch and Connect to EC2

Launch an Ubuntu EC2 instance in AWS and connect through SSH.

### 2. Prepare the Environment

```bash
sudo apt update
sudo apt install ansible git -y
ansible --version
```

### 3. Clone the Repository

```bash
git clone https://github.com/atharvag25/ansible-devops-project.git
cd ansible-devops-project
```

### 4. Configure Inventory (`inventory.ini`)

```ini
[webservers]
localhost ansible_connection=local
```

### 5. Configure the Playbook (`playbook.yml`)

```yaml
---
- name: Configure Nginx Web Server
  hosts: webservers
  become: yes

  tasks:
    - name: Update package cache
      apt:
        update_cache: yes
        cache_valid_time: 3600

    - name: Install Nginx
      apt:
        name: nginx
        state: present

    - name: Start and enable Nginx
      service:
        name: nginx
        state: started
        enabled: yes

    - name: Deploy custom HTML webpage
      copy:
        src: index.html
        dest: /var/www/html/index.html
        owner: www-data
        group: www-data
        mode: '0644'
```

### 6. Validate and Execute

**Check inventory connectivity:**

```bash
ansible webservers -i inventory.ini -m ping
```

**Check playbook syntax:**

```bash
ansible-playbook -i inventory.ini playbook.yml --syntax-check
```

**Execute the playbook:**

```bash
ansible-playbook -i inventory.ini playbook.yml
```

### 7. Verify Deployment

**Check Nginx service:**

```bash
ansible webservers -i inventory.ini -m command -a "systemctl is-active nginx"
```

Expected output: `active`

**Open the deployed webpage:**

```text
http://YOUR-EC2-PUBLIC-IP
```

Ensure that inbound HTTP traffic on TCP port 80 is allowed in the EC2 security group.

## Implementation Results

- Ansible inventory connectivity test: Successful.
- Playbook syntax validation: Successful.
- Nginx installation and service configuration: Successful.
- Custom HTML webpage deployment: Successful.
- Nginx service status: `active`.
- Playbook execution: Zero failed and zero unreachable tasks.
- Webpage: Successfully accessible through the EC2 public IPv4 address.

## Project Architecture

The same EC2 Ubuntu instance acts as both the Ansible control node and managed target through `ansible_connection=local`. Nginx serves the deployed webpage from `/var/www/html/index.html`.

## Repository Structure

```text
ansible-devops-project/
├── .gitignore
├── README.md
├── index.html
├── inventory.ini
└── playbook.yml
```

## Repository

[GitHub – ansible-devops-project](https://github.com/atharvag25/ansible-devops-project)

**Author:** Atharva Gavali
