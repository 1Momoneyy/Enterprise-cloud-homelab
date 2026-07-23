# Ticket 003 - Create and Associate a Network Security Group

## Business Objective

Secure the management subnet before deploying any virtual machines by creating and associating a Network Security Group (NSG).

---

## Resources Created

**Resource Type:** Network Security Group

**Name:** nsg-management

**Region:** East US 2

**Resource Group:** rg-enterprise-cloud-lab-dev

---

## Configuration

The Network Security Group was associated with the following subnet:

**Virtual Network**
vnet-enterprise-cloud-lab-dev

**Subnet**
snet-management

---

## Why We Created It

A Network Security Group (NSG) acts as a virtual firewall in Azure.

It controls which network traffic is allowed to enter and leave Azure resources.

Associating the NSG with the management subnet ensures that every virtual machine deployed into that subnet inherits the same security rules.

---

## What I Learned

I learned that creating an NSG alone is not enough. The NSG must be associated with a subnet or network interface before it protects any resources.

By attaching the NSG to the management subnet, future virtual machines deployed into that subnet will automatically be protected by the configured security rules.

---

## Skills Practiced

- Azure Networking
- Network Security Groups (NSGs)
- Subnet Security
- Network Segmentation
- Infrastructure Design
## Resources Created During This Ticket

- Network Security Group
    - nsg-management

## Existing Environment

Azure Subscription
└── rg-enterprise-cloud-lab-dev
    ├── vnet-enterprise-cloud-lab-dev
    │   └── snet-management
    │       └── nsg-management