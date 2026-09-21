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