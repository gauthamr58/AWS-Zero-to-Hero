# AWS VPC
<img src="https://github.com/gauthamr58/AWS-Zero-to-Hero/blob/main/assets/vpc.png" alt="Banner" />

## What is a VPC?

A **Virtual Private Cloud (VPC)** is a **logically isolated virtual network** within the AWS Cloud where you can launch and manage AWS resources securely.

A VPC allows you to define: 

* Your own IP address range
* Subnets ( public and private)
* Route tables
* Internet and NAT gateways
* Network security controls

In simple terms a VPC is **your private network in AWS**, similar to an on-premise data centre network.

---

## Why do we need a VPC?

A VPC is required to achieve **security, isolation, and network control**.

Key reasons:

* **Network isolation** from other aws customers
* **Private IP addressing** for resources
* **Controlled internet access** (public vs private subnets)
* **Fine grained security** (using security Groups and NACLs)
* **High availability** using multiple availablity zones
* **Hybrid connectivity** ( VPN / Direct connect with on premise)

Without VPC its impossible to deisgn secure, scalable production-ready architecture in AWS.

---

## VPC CIDR Block (IP Addressing)

When creating a VPC, you must assign an **IPv4 CIDR block** that defines the IP address range for the VPC.

### Private IPv4 CIDR ranges Allowed (RFC 1918)

* '10.0.0.0/8'
* '172.16.0.0/12'
* '192.168.0.0/16'

### CIDR Mask Bit Range Allowed in AWS VPC

* **Minimum:** `/16`
* **Maximum:** `/28`

This means:

* Largest VPC: `/16` → 65,536 IP addresses
* Smallest VPC: `/28` → 16 IP addresses

⚠️ The primary CIDR block **cannot be modified** after VPC creation (only additional CIDRs can be added).

---

## What is a Subnet?

A **subnet** is a range of IP addresses in your VPC. A subnet must reside in a single Availability Zone. After you add subnets, you can deploy AWS resources in your VPC.

---

## Reserved IPs in AWS VPC

AWS reserves **5 IP addresses in every subnet**, and these IPs **cannot be assigned** to resources.

For a subnet CIDR block:

```
Example: 10.0.1.0/24
```

| Reserved IP  | Purpose                 |
| ------------ | ----------------------- |
| `10.0.1.0`   | Network address         |
| `10.0.1.1`   | VPC router              |
| `10.0.1.2`   | AWS DNS                 |
| `10.0.1.3`   | Reserved for future use |
| `10.0.1.255` | Broadcast address       |

👉 Even though AWS does not use traditional broadcasting, the last IP is still reserved.

---

## What is defaulf VPC and Its Specifications?

A **Default VPC** is an automatically created VPC by AWS for every region.

### Default VPC Specifications

* **CIDR Block:** '172.31.0.0/16'
* **Subnets:** one public subnet per Availability Zone
* **Internet Gateway:** Attached by default
* **Rouote Table:** Routes internet traffic to IGW
* **Security Group:** Default SG allows inbound trafiic from itself
* **NACL:** Default NACL allows all inbound and outbound traffic
* **Public IP:** EC2 instances get public IP by default

## Components automaically created when we create a VPC

When you create a Virtul Private Cloud (VPC) in AWS, it doesn't just create an empty shell. To ensure the network is functional and manageable from the start, AWS automatically provisions several "default" components.

## 1. Default Route Table

Every VPC must have a route table to direct network traffic. Upon creation, AWS generates a **Main Route Table**.

* **Purpose:** It acts as the default routing logic for any subnet you create later that isn't explicitly associated with a different route table.
* **Initial Rule:** It comes with a single "local" route that allows communication between all resources within the VPC CIDR block.
  
## 2. Default Network ACL (NACL)

A Network Access Contol List (NACL) is an optional layer of security for your VPC, that acts as a firewall for controlling traffic in and out of one or more subnets.

* **Default Behavior:** Unlike custom NACLs which deny all trafFic by default, the **Default NACL** is configured to **allow all inbound and outbound traffic**.
* **Scope:** It is automatically applied to any new subnet you create unless you specify otherwise.

## 3. Default Security Group
A Security group acts as a virtual firewall for your instances (at the ENI level).

* **Inbound Rules:** It allows all traffic from resources that are assigned to the **same security group**.
* **Outbound Rules:** It allows all outbound traffic to any destination.
* **Note:** If you launch an instance and don't specify a security group, this default one is automatically       attached to it.

## 4. Main DHCP Options set

To ensure your instances can communicate over the network using domain names, AWS creates and associates a DHCP (Dynamic Host Configuration Protocol) options set.

* **Function:** This provides instances with configurations like domain name servers (AmazonProvideDNS), Domain names, NTP servers.

---

### What is NOT created automatically? 
It is just as important to know what you have to build yourself. when you create a VPC via the API or "VPC Only" console option, the following are **missing:**

* **Subnets:** You must define your own public or private subnets.
* **Internet Gateway (IGW):** Your VPC has no internet access by default.
* **NAT Gateways:** Required if you want private subnets to reach the internet.
