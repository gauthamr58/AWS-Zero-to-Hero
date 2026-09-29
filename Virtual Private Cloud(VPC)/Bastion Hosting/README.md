
# Bastion Hosting
<img src="https://github.com/gauthamr58/AWS-Zero-to-Hero/blob/main/assets/bh.png" alt="Banner" />


## 1. What is a Bastion Host?

A **bastion host** is a specially configured server designed to withstand attacks and serve as a secure entry point into a private network. It is hardened, monitored, and exposed to untrusted networks (like the public internet) so that internal system remain isolated and protected.

The term *bastion* comes from military usage - a fortified position designed to defend against direct attacks. In networking, it plays the same role: a secure access gateway.

---

## 2. **Why Use a bastion Host?**

The primary goals of using a bastion host are:

✔ **Secure Access:** Provides controlled adinistrative access (SSH/RDP) into internal systems.

✔ **Network Isolation:** Keeps direct access to private resources restricted.

✔ **Threat Surface Reduction:** Limits entry points exposed to public networks.

✔ **Audit and Accountability:** Centralizes logging of access events.

Without a bastion host, administrative access might be opened directly to each host in private networks, significally incresing risk.

---

## **3. Typical Use Cases**

| Scenario                           | Role of Bastion Host                           |
| ---------------------------------- | ---------------------------------------------- |
| Managing private servers (SSH/RDP) | Acts as the only externally accessible host    |
| Regulatory compliance              | Records and enforces access auditing           |
| Zero Trust Architecture            | Enforces least-privilege access                |
| Hybrid cloud environments          | Provides secure bridge between on-prem & cloud |

---

## 4. How it works?

### Netwok Architecture

A typical architecture using a bastion host:

'''
Internet
    |
Public Subnet ( Bastion Host)
    |
Private Subnet (App servers/ Databases)
'''

Only the bastion Host has a **public IP**. Internal servers reside inside **private subnets** with no direst internet exposure.

### **Access Flow**

1. Administrator connects to the bastion host (SSH/RDP).
2. From the bastion, a second connection is made to internal servers.
3. Internal hosts are never exposed directly to the internet.

---

## **5. Security Hardening Best Practices**

A bastion host must be **hardened** to resist attacks:

### **Authentication**

* Use **SSH key pairs**, not passwords
* Prefer **MFA (Multi-Factor Authentication)**
* Integrate with identity providers (LDAP/Active Directory)

### **Network Controls**

* Allow inbound only from trusted IP ranges
* Restrict outbound so that the bastion can only reach internal systems it needs
* Use security groups/firewalls

### **Operating System Hardening**

* Disable unused services/ports
* Keep OS and packages updated
* Enforce strong password policies (if any)

### **Logging & Monitoring**

* Enable verbose auth logs
* Send logs to a central system (SIEM, CloudWatch, Splunk)
* Alert on suspicious activity (multiple failed logins, unusual times)

### **Session Management**

* Use jump host session recording
* Restrict session timeouts
* Periodically rotate SSH keys


#🧪 LAB: Checking Internet Connectivity of a Private EC2 Using Bastion Host (AWS)

## 🏗️ Step 1: Create VPC Architecture

### 1️⃣ Create VPC

Go to **VPC → Create VPC**

* Name: `bation-lap-vpc`
* IPv4 CIDR: `10.0.0.0/16`
* Tenancy: Default

---

## 2️⃣ Create Subnets

### Public Subnet

* Name: `public-subnet`
* AZ: Any (e.g., ap-south-1a)
* CIDR: `10.0.1.0/24`
* Enable: **Auto-assign Public IP**

### Private Subnet

* Name: `private-subnet`
* AZ: Same AZ/Different AZ
* CIDR: `10.0.2.0/24`

---
## Create Private & Public Routetables

- Route tables - create - Private RT - Select VPC - Create - Associate the RT with appropriate subnet
- Route tables - create - Public RT - Select VPC - Create - Associate the RT with appropriate subnet

## 3️⃣ Create Internet Gateway (IGW)

Go to **Internet Gateway → Create**

* Name: `bastion-igw`
* Attach to `bastion-lab-vpc`

---