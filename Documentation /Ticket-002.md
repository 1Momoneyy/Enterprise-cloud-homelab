# Ticket 002 - Create Azure Virtual Network

## Objective

Create the private network that will host all infrastructure for the Enterprise Azure Cloud Homelab.

---

## Resources Created

Virtual Network

Name:
vnet-enterprise-cloud-lab-dev

Address Space:
10.0.0.0/16

Region:
East US 2

---

## Subnet Created

Name:
snet-management

Address Range:
10.0.0.0/24

---

## Why We Created It

The Virtual Network provides a secure private network where Azure resources can communicate.

The Management Subnet separates management resources from future workloads such as web servers and databases.

---

## What I Learned

A Virtual Network is the foundation of Azure networking.

Subnets divide the network into smaller logical sections, making the environment easier to organize, secure, and scale.