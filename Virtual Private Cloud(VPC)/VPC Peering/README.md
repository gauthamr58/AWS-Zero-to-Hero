
# What is VPC Peering?

AWS VPC peering is a network connection between two VPCs that enables them to route traffic privately using private IP addresses. 

It works:
* Within the same region 
* Across regions (Inter-Region Peering)
* Same account or different accounts

No traffic goes through the public internet. 

---

# 2️⃣ Architectural Overview 

<img src="https://github.com/gauthamr58/AWS-Zero-to-Hero/blob/main/assets/vpcpeering.png" alt="Banner" />

Example:

VPC-A (10.0.0.0/16)
VPC-B (192.168.0.0/16)

After peering:

* Add Route in VPC-A → 192.168.0.0/16 → peering connection
* Add Route in VPC-B → 10.0.0.0/16 → peering connection

Now instances communicate privately. 

---

# Key Requirements

### ✅ 1. CIDR must NOT overlap

Example:

* VPC1: 10.0.0.0/16
* VPC2: 10.0.0.0/16 ❌ (Not allowed)

### ✅ 2. Route tables must be updated manually

you must explicitly update the Route Tables for both VPCs.

### ✅ 3. Security groups and firewall must be updated

You must update the security groups or firewall rules in both VPCs to explicitly allow inbound/outbound traffic from the peer VPC's IP range or specific application ports 
(e.g., allowing port 443 or 5432 for database access).

### ✅ 4. IAM Permissions / Administrative Access

You must have the appropriate administrative permissions or Identity and Access Management (IAM) roles in both VPCs to create and modify peering connections, routing tables, and security groups.

### ✅ 5. DNS Resolution Settings (Optional but Recommended)

If your applications rely on private DNS hostnames to communicate across VPCs, you must enable DNS resolution (and sometimes hostname support) on the peering connection settings so that instances can resolve each other's private DNS names across the boundary

Peering does NOT automatically update:

* Route tables
* Security groups
* NACLs

---




