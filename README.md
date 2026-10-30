# Automating Web Server Configuration on AWS EC2 Using Ansible

## 1. Project Overview

This project demonstrates automated installation, configuration, and deployment of an Nginx web server on an AWS EC2 Ubuntu instance using Ansible.

Ansible automates package updates, Nginx installation, service management, and deployment of a custom HTML webpage.

## 2. Technologies Used

- **Cloud Platform:** Amazon Web Services (AWS)
- **Compute Service:** Amazon EC2
- **Operating System:** Ubuntu Linux
- **Configuration Management:** Ansible
- **Web Server:** Nginx
- **Version Control:** Git and GitHub
- **Web Technologies:** HTML and CSS

## 3. Project Architecture

The project uses an AWS EC2 Ubuntu instance as the Ansible control node. Ansible manages the local machine using a local connection.

**Workflow:**

1. Launch an Ubuntu EC2 instance on AWS.
2. Connect to the instance.
3. Install Ansible.
4. Configure the Ansible inventory.
5. Execute the Ansible playbook.
6. Install and configure Nginx.
7. Deploy the custom HTML webpage.
8. Access the webpage through the EC2 public IPv4 address.

## 4. Repository Structure

```text
ansible-devops-project/
│
├── index.html       # Custom webpage
├── inventory.ini    # Ansible inventory
├── playbook.yml     # Ansible automation playbook
├── .gitignore       # Files excluded from Git
└── README.md        # Project documentation
```

## 5. Prerequisites

- An AWS account.
- An Ubuntu EC2 instance.
- Ansible installed on the EC2 instance.
- Git installed.
- Inbound security group rule allowing SSH (TCP 22) from the authorized IP.
- Inbound security group rule allowing HTTP (TCP 80).

## 6. Installation and Configuration

### Step 1: Update Ubuntu

```bash
sudo apt update
sudo apt upgrade -y
```

### Step 2: Install Ansible and Git

```bash
sudo apt install ansible git -y
```

Verify Ansible:

```bash
ansible --version
```

### Step 3: Clone the Repository

```bash
git clone https://github.com/atharvag25/ansible-devops-project.git
cd ansible-devops-project
```

### Step 4: Configure the Inventory

The `inventory.ini` file defines the target host.

```ini
[webservers]
localhost ansible_connection=local
```

### Step 5: Validate Ansible Connectivity

```bash
ansible webservers -i inventory.ini -m ping
```

### Step 6: Validate the Playbook Syntax

```bash
ansible-playbook -i inventory.ini playbook.yml --syntax-check
```

### Step 
