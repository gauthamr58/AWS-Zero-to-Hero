
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
