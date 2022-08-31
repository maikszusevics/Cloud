# NACL
### __Network access control list__
---
This is a security management tool, almost akin to a security group but used for subnets instead of instances. It is a firewall to protect the subnet.

#### Difference between NACL and securtiy groups:
- NACL assigned to subnets not isntances
- SG first layer of defence, NACL second layer of defence
- SG denies all rules by default, exceptions are configured, NACL denial rules are configured
- Security group rule allow CIDR, IP, Security group as destination, NACL allow only CIDR as destination

---
## Stateless & Stateful
**Stateless**:

Network ACLs are stateless. This means any changes applied to an incoming rule will not be applied to the outgoing rule. e.g. If you allow an incoming port 80, you would also need to apply the rule for outgoing traffic.


**Stateful**:

Security groups are stateful. This means any changes applied to an incoming rule will be automatically applied to the outgoing rule. e.g. If you allow an incoming port 80, the outgoing port 80 will be automatically opened.


