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

## Documentation

Nextcloud running via SSH tunnel.
[dokumentation.md](https://github.com/user-attachments/files/25826051/dokumentation.md)
**Documentation – Grand Lab**



**In this lab, I established a cloud infrastructure in OpenStack using Terraform, which allows for Infrastructure as Code. The objective was to develop a private network that includes a bastion server and an internal server running Nextcloud.**



**I began by creating the network elements using Terraform. I set up a private network (10. 20. 0. 0/24), a subnet, and a router connected to external-net. The router enables instances within the private network to communicate with external-net and utilize floating IP addresses.**



**Next, I launched two instances with Terraform: a bastion server and a Nextcloud server. The bastion server received a floating IP address (198. 18. 3. 207) and serves as the entry point to access the environment via SSH. I connect to the bastion using:**



**ssh -i keys/labkey ubuntu@198. 18. 3. 207**



**The Nextcloud server is confined to the private network and does not have a floating IP address. This means it cannot be accessed directly from the internet; rather, it can only be reached through the bastion.**



**Both instances are part of the same security group (bastion-sg). This group permits only SSH traffic (TCP port 22) from all IP addresses. Consequently, the Nextcloud server is not publicly accessible as it lacks a floating IP and is only reachable through the internal network.**



**Nextcloud was installed directly on the Nextcloud server after the instance was set up. Once I logged in via SSH, I installed Apache and launched the web server to ensure the service listens on port 80. This was confirmed by running:**



**sudo ss -tlnp | grep :80**



**To access Nextcloud from my workstation, I used an SSH tunnel through the bastion server. I established the tunnel with the command:**



**ssh -i keys/labkey -N -L 8080:10. 20. 0. 243:80 ubuntu@198. 18. 3. 207**



**This tunnel forwards local port 8080 to port 80 on the Nextcloud server via the bastion. Later, I was able to open Nextcloud in my web browser using:**



**http://localhost:8080**



**I confirmed the application was functioning by logging into Nextcloud and checking the dashboard. I have attached screenshots that show the entire browser window, displaying my login to the application.**



**In conclusion, I utilized Terraform to create the network, router, and instances within OpenStack. The bastion server is used for SSH access to the environment, while the Nextcloud server resides in the private network without a public IP address. Nextcloud was manually set up on the server and is accessible through an SSH tunnel via the bastion.**


