# Active Directory Homelab – Phase 1 (AD DS, DNS, DHCP)

## Project Overview
This project documents the deployment, configuration, troubleshooting, and validation of a Windows Server 2019 Active Directory homelab environment.

The goal of this phase was to build a functional Domain Controller and validate core infrastructure services required for an enterprise-style Windows environment.

### Core services deployed
- Active Directory Domain Services (AD DS)
- DNS (Domain Name System)
- DHCP (Dynamic Host Configuration Protocol)

A Windows 11 client was used to validate:
- DHCP lease assignment
- DNS name resolution
- Domain Controller discovery
- readiness for domain join

---

## Lab Environment

### Server
- **OS:** Windows Server 2019
- **Hostname (final):** `Server_2019_DC01`
- **IP Address:** `10.10.10.1`
- **Subnet:** `255.255.255.0`
- **Preferred DNS:** `10.10.10.1`

### Domain
- **Domain Name:** `local.lab`
- **Forest Name:** `local.lab`
- **Forest Functional Level:** Windows Server 2016
- **Domain Functional Level:** Windows Server 2016

### Client
- **OS:** Windows 11
- **Hostname:** `PC_01_Local`
- **IP Assignment:** DHCP

---

## Objectives
- Deploy a Windows Server 2019 Domain Controller
- Install and configure AD DS, DNS, and DHCP
- Validate DHCP scope assignment to the client
- Validate DNS name resolution from the client
- Troubleshoot Domain Controller discovery issues
- Confirm successful DC locator and Active Directory service discovery
- Prepare the environment for:
  - domain join
  - OU and user creation
  - Group Policy testing

---

## Key Validation Performed

### DHCP Validation
The Windows 11 client successfully received:
- an IP address in the lab subnet
- DNS server address `10.10.10.1`
- DHCP server address `10.10.10.1`

### Connectivity Validation
The client successfully pinged the Domain Controller IP:
- `10.10.10.1`

This confirmed:
- Layer 3 connectivity
- basic client-to-server communication
- internal lab network reachability

### DNS Validation
Initial DNS testing showed that the client could reach the DNS server, but resolution health was not fully correct during early validation.

The server was initially named:
- `Server_2019_DC`

It was later renamed to:
- `Server_2019_DC01`

This introduced a temporary mismatch between the hostname, DNS registration, and AD-related service records.

---

## Issue Encountered
Although basic connectivity and partial DNS resolution were working, the client initially failed to discover the Domain Controller using Active Directory DC locator.

### Command used
```cmd
nltest /dsgetdc:local.lab