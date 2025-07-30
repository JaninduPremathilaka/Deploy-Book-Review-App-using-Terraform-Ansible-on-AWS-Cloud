
# Book Review App on Azure Cloud 🚀  
### Full-Stack Deployment using **Terraform**, **Ansible**, and **Azure Virtual Machines**

## 📘 Overview

This is a **customized, cloud-hosted version** of the Book Review App — a full-stack, three-tier web application that enables users to browse books and submit reviews.

🔧 **Deployed by**: Janindu Premathilaka  
📦 **Tools Used**: Terraform, Ansible, Azure CLI, Git

Based on the structure taught in the Udemy course *[DevOps Zero to Hero: Docker, K8s, Cloud, CI/CD & 4 Projects](https://www.udemy.com/user/pravin-mishra-30/)*, this project demonstrates **infrastructure provisioning + app configuration + deployment automation** using real-world DevOps workflows.

---

## 🏗️ Architecture

- **Infrastructure**: Azure VMs, NSGs, Public IP, NICs (via Terraform)
- **App Stack**:  
  - Frontend: Next.js  
  - Backend: Node.js + Express  
  - Database: MySQL  
- **Configuration Management**: Ansible (multi-playbook structure)
- **CI/CD**: Manual deployment with Terraform + Ansible (can be upgraded to pipelines)

---

## 🌐 Features

### 🧑‍💻 Authentication
- Register / login with email-password
- Auth state managed via JWT and React Context

### 📚 Book Management
- View list of books
- Book detail view and reviews

### 📝 Reviews
- Logged-in users can post reviews
- Rating, timestamp, username displayed

---

## 💻 Project Structure

```
book-review-app/
 ├── frontend/               # Next.js frontend
 ├── backend/                # Express.js backend
 ├── terraform/              # Infra-as-Code (Azure)
 │    ├── main.tf
 │    ├── variables.tf
 │    ├── terraform.tfvars
 │    └── outputs.tf
 ├── ansible/                # Automation config
 │    ├── inventory.ini
 │    └── webserver-installation.yml
 └── README.md               # This file
```

---

## 📦 Tech Stack

### Application
- **Frontend**: Next.js, Tailwind CSS, Axios
- **Backend**: Node.js, Express, Sequelize (MySQL), JWT
- **Database**: MySQL

### DevOps
- **Terraform**: Azure infrastructure provisioning  
- **Ansible**: Web server provisioning, app deployment  
- **Azure**: Cloud provider  
- **GitHub**: Code source and cloning

---

## 🛠️ Prerequisites

Ensure the following are installed on your local machine:
- [Terraform](https://developer.hashicorp.com/terraform/downloads) (v1.0+)
- [Ansible](https://docs.ansible.com/)
- [Azure CLI](https://learn.microsoft.com/en-us/cli/azure/install-azure-cli)
- SSH Key Pair (`~/.ssh/id_rsa` and `id_rsa.pub`)
- Git

Then run:

```bash
az login
```

---

## 🚀 Step-by-Step Deployment

### 1️⃣ Provision Infrastructure (Terraform)

Navigate to the `terraform/` directory and initialize:

```bash
cd terraform
terraform init
terraform plan -var-file="terraform.tfvars"
terraform apply -var-file="terraform.tfvars"
```

> ⚠️ Note: After apply, copy the `public_ip_address` output to update the Ansible inventory.

---

### 2️⃣ Configure Server & Deploy App (Ansible)

Update the `ansible/inventory.ini` file:

```ini
[web]
<Your_Public_IP_From_Terraform>

[all:vars]
ansible_user=azureuser
ansible_ssh_private_key_file=~/.ssh/id_rsa
ansible_python_interpreter=/usr/bin/python3
```

Then run the Ansible playbook:

```bash
cd ../ansible
ansible-playbook -i inventory.ini webserver-installation.yml
```

This will:

- Install Nginx
- Clone the Book Review App (or your repo)
- Copy frontend + backend into proper locations
- Configure and restart the Nginx web server

---

## 🌍 Access the App

After deployment:
- 🌐 App URL: `http://<Your_Public_IP>`

---

## 📚 Learning Outcome

- Designed real-world cloud architecture with Azure
- Used **Terraform** to automate infrastructure provisioning
- Used **Ansible** to automate multi-step app deployment
- Gained exposure to IaC, SSH, Web Server setup, and full-stack app management

---

## 🧠 Extra Notes

- You can easily extend this setup with:
  - GitHub Actions for CI/CD
  - Azure Load Balancer for scalability
  - Azure Database for managed MySQL
  - Docker/K8s for containerized deployment

---

## 📢 Credits

App concept based on the Udemy course [DevOps Zero to Hero](https://www.udemy.com/user/pravin-mishra-30/).  
Terraform + Ansible deployment logic guided by **Mini Finance Lab** in the same course.

**Customized and deployed independently by Janindu Premathilaka.**

---

## 🔗 Useful Links

- [Frontend README](./frontend/README.md)
- [Backend README](./backend/README.md)
- [Terraform Docs](./terraform/)
- [Ansible Playbook](./ansible/)

## 🛠️ Getting Started

1. **Fork** and **clone** this repository to your local environment.  
2. ⭐ **Star** the repository to show your support and follow updates.

---

## 📌 Connect with Me

- 💼 [LinkedIn – Janindu Premathilaka](https://www.linkedin.com/in/janindupremathilaka)

---