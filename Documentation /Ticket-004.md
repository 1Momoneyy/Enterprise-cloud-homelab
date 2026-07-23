# Ticket 004 – Deploy Ubuntu Linux Management Server

## Objective

Deploy a secure Ubuntu Linux virtual machine in Microsoft Azure to serve as the primary Linux management server for the Enterprise Cloud Lab.

---

## Environment

Subscription:
Azure Subscription 1

Region:
East US 2

Resource Group:
rg-linux-management

Virtual Machine:
vm-linux-management-01

Operating System:
Ubuntu Server 24.04 LTS

---

## Compute

VM Size:
Standard_D2s_v3

Specifications

- 2 vCPUs
- 8 GB RAM

Reason for Selection

Originally planned to deploy a B-Series virtual machine. Azure quota restrictions prevented deployment, so Standard_D2s_v3 was selected instead.

---

## Authentication

Authentication Method

SSH Public Key

SSH Key Type

ED25519

Administrator Username

mohamed bah

---

## Storage

OS Disk

Standard SSD

Encryption

Platform Managed Keys

---

## Networking

Connected to

Virtual Network:
vnet-eastus2-1

Subnet:
snet-eastus2-1

Network Security

Network Security Group attached

Public IP assigned

SSH (TCP Port 22) enabled

---

## Deployment Status

Deployment completed successfully.

Resources created

- Virtual Machine
- Network Interface
- Public IP Address
- Network Security Group
- Managed Disk

---

## Skills Demonstrated

- Azure Virtual Machines
- Azure Compute
- Azure Networking
- SSH Authentication
- Linux Infrastructure Deployment
- Cloud Administration
- Resource Group Management

---

## Lessons Learned

Azure quota restrictions may prevent deployment of certain VM families.

Alternative VM sizes can be selected without impacting the overall project architecture.

Using SSH keys instead of passwords provides stronger authentication and follows security best practices.

---

## Next Ticket

Ticket 005

Connect to the Linux VM via SSH and perform initial server configuration.

