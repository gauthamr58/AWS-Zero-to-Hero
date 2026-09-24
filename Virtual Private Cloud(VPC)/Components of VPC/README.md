
# AWS VPC – Components 

## 1. What is an AWS VPC?

An **Amazon Virtual Private Cloud (VPC)** is a logically isolated virtual network in AWS where you can launch AWS resources such as EC2 instances, RDS, and load balancers.
You control:

* IP addressing
* Subnets
* Routing
* Network gateways
* Security boundaries

A VPC closely resembles a traditional on-premises network but with cloud scalability.

---

## 2. Subnet in AWS VPC
<img src="https://github.com/gauthamr58/AWS-Zero-to-Hero/blob/main/assets/subnet.png" alt="Banner" />


### What is a Subnet?

A **subnet** is a range of IP addresses within a VPC.
Subnets allow you to **divide your VPC network into smaller segments**.

Key points:

* A subnet is **always created inside one Availability Zone (AZ)**
* You cannot span a subnet across multiple AZs
* Each subnet uses a CIDR block derived from the VPC CIDR

---

### Reserved IP Addresses in a Subnet

AWS reserves **5 IP addresses** in every subnet:

* Network address (first IP)
* VPC router
* DNS
* Future use
* Broadcast address (last IP)

Example:
CIDR: `10.0.1.0/24`
Usable IPs: `251`

---

### Types of Subnets

#### 1️⃣ Public Subnet

A subnet is **public** if:

* Its route table has a route to an **Internet Gateway (IGW)**

Used for:

* Web servers
* Bastion hosts
* Load balancers

Example route:

```
0.0.0.0/0 → Internet Gateway
```

---

#### 2️⃣ Private Subnet

A subnet is **private** if:

* It does NOT have a direct route to the Internet Gateway

Used for:

* Application servers
* Databases
* Internal services

Internet access (outbound only) is possible via **NAT Gateway**.

---