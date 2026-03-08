# openstack-nextcloud-bastion-lab
Infrastructure as Code lab using Terraform on OpenStack with a bastion host and internal Nextcloud server accessed via SSH tunneling.

This project demonstrates how to deploy a segmented cloud environment in OpenStack using Terraform.

The infrastructure includes:

- Private network (10.20.0.0/24)
- Router connected to external-net
- Bastion host with floating IP
- Internal Nextcloud server without public IP
- SSH tunneling for secure access

The goal of the lab was to build a secure architecture where the application server is not exposed directly to the internet.

## Architecture

Local Machine
↓
WireGuard VPN
↓
Floating IP (Bastion)
↓
Private Network
↓
Nextcloud Server

The bastion host acts as a jump host to access the internal server.

## SSH Access

Connect to bastion:

Create SSH tunnel to Nextcloud: ssh -i keys/labkey -N -L 8080:10.20.0.243:80 ubuntu@198.18.3.207


Access the application:
http://localhost:8080


## Technologies Used

- OpenStack
- Terraform
- Linux
- SSH
- Nextcloud
- Infrastructure as Code

## Nextcloud Dashboard

Application running through SSH tunnel.

Full Browser Window

## Repository Structure
terraform/
  provider.tf
  network.tf
  compute.tf
  locals.tf

documentation/
  documentation.md

screenshots/
  nextcloud-dashboard.png
  nextcloud-browser.png
  openstack-instance.png

## Learning Outcomes

Through this lab I practiced:

Deploying infrastructure using Terraform

Designing segmented cloud networks

Working with bastion architectures

Managing secure remote access using SSH tunnels

## .gitignore

.terraform/
*.tfstate
*.tfstate.backup
*.pem
labkey
keys/
Deploying and verifying a web application in a private network
