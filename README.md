# ACIT 4640 Lab 7 – Ansible Nginx Deployment

## Overview

This lab uses Terraform to provision two AWS EC2 instances and Ansible to install and configure nginx on both servers. Ansible copies the nginx configuration file, creates the required web directory, deploys a templated index.html file, and reloads and enables the nginx service.

---

## SSH Key Commands

### Create SSH key pair

Creates a new SSH key pair named "aws" for connecting securely to EC2 instances.

```bash
ssh-keygen -t ed25519 -f ~/.ssh/aws -C "aws"
```

### Import SSH key into AWS

Imports the public key into AWS so Terraform can create EC2 instances that trust this key.

```bash
./scripts/import_lab_key ~/.ssh/aws.pub
```

### Delete SSH key from AWS

Deletes the SSH key from AWS after completing the lab.

```bash
./scripts/delete_lab_key
```

---

## Terraform Commands

### Initialize Terraform

Initializes Terraform and downloads required providers.

```bash
terraform init
```

### Format Terraform files

Formats Terraform configuration files for consistency.

```bash
terraform fmt
```

### Validate Terraform configuration

Checks Terraform configuration for syntax and errors.

```bash
terraform validate
```

### Plan Terraform deployment

Shows what infrastructure Terraform will create.

```bash
terraform plan
```

### Apply Terraform configuration

Creates the EC2 instances and networking infrastructure.

```bash
terraform apply
```

---

## Ansible Commands

### Syntax check playbook

Checks the playbook for syntax errors before running.

```bash
ansible-playbook -i ansible/inventory/hosts.yml ansible/playbook.yml --syntax-check
```

### Run playbook

Installs nginx, copies configuration files, creates the web page, and reloads nginx.

```bash
ansible-playbook -i ansible/inventory/hosts.yml ansible/playbook.yml
```

---

## Screenshot of deployed webpage

The screenshot below shows the nginx web server successfully serving the templated webpage.

![Nginx Screenshot](docs/screenshot.jpg)

---

## Cleanup

### Destroy infrastructure

Removes all AWS infrastructure created by Terraform.

```bash
terraform destroy
```

### Delete SSH key

Removes the SSH key from AWS.

```bash
./scripts/delete_lab_key
```

