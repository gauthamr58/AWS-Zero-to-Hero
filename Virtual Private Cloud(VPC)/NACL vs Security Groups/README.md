
# 🔐 NACL vs Security Groups in AWS
Security groups are stateful, instance-level firewalls, whereas network ACLs are stateless, subnet-level firewalls. 
In an AWS VPC, both security groups and network ACLs control inbound and outbound traffic. However, they operate at different layers of the network stack and serve distinct purposes in a defense-in-depth security model. 

---

## 📍 Architectural placement 

![Image](https://cloudviz.io/assets/aws-security-group-vs-nacl/security-groups.png)

![Image](https://docs.aws.amazon.com/images/vpc/latest/userguide/images/network-acl.png)