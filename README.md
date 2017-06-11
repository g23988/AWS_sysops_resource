
# AWS_sysops_resource
for AWS Certified Sysops - Associate exam


## 重點節錄


## 官方範例


## 有用的範例問題
```
To be prepared for a security assessment, an organization should implement which two configuration management practices?

Choose 2 answers

A) Determine whether remote administrative access is performed securely.

B) Verify that all Amazon Simple Storage Service (53) bucket policies and ACLs correctly implement your security policies

C) Determine whether unnecessary users and services have been identified on all Amazon-published AMIs.

D) Verify that AWS Trusted Advisor has identified and disabled all unnecessary users and services on your Amazon Elastic Compute Cloud (EC2) instances.
```
> A & B

Read the Security whitepaper and the Security Best Practice whitepaper.

Intro to AWS Security is also quite good.

-- [Security Best Practice whitepaper](https://d0.awsstatic.com/whitepapers/Security/AWS_Security_Best_Practices.pdf)


---------------------------------------------------




```
A customer would like to host some of their corporate servers in Amazon Web Services and have chosen to create a VPC deployment as an extension of their on-premises data center. The existing on-premises data center already has multiple redundant DNS servers. These DNS servers are hosting DNS records for several internal applications, such as mail servers and business applications. The corporate security policy specifies that the DNS names for the internal applications can only be resolved within the secure internal corporate network through the on-premises DNS server and cannot be resolved over the public internet or through a Public DNS server. The on-premises DNS servers can resolve Internet domain names through recursion. Secure network connectivity between the VPC and the on-premises data center has been established using IPSec VPN.

The Amazon Elastic Compute Cloud (EC2) instances that are launched within this VPC will host applications that frequently connect to the corporate applications hosted in the on-premises data center. The enterprise policy mandates the use of domain names to connect to all internal applications.

Select the option that is most effective for building a scalable DNS architecture:

A. Create a new Route 53 hosted zone for the internal domain and add all internal domain names as record sets in the Route 53 hosted-zone. Modify the default DHCP option set for the VPC to specify the domain name server value as Route 53.

B. Create a new Route 53 hosted zone for the internal domain name, and configure Route 53 to forward all DNS queries for internal domain names to the on-premises DNS servers. Modify the default DHCP option set for the VPC to specify the domain name server value as Route 53.

C. Create a new DHCP option set that specifies the domain name server value as the on-premises DNS servers. Replace the default DHCP option set for the VPC with the newly created DHCP option set.

D. Create two DHCP options sets, DHCPSetA and DHCPSetB. Configure DHCPSetA to specify the Amazon-provided DNS server as the domain name server to resolve all Internet domain names. Configure DHCPSetB to specify the on-premises DNS server as the domain name server to resolve all internal domain names. Apply both the DHCP options set to the VPC so that both Internet domain names and internal domain names can be resolved.
```
> C

```
It is "C", because it says the on-premises DNS servers can resolve Internet domain names through recursion, so we dont need to do anything additional to having the VPC resolve everything through the on-premises DNS servers.

In other words, Instance A in the private VPC tries to resolve "google.com" -> ask on-premises DNS servers -> not found -> recurively exhaust options until it searches the public internet domain.


The answer is very loud and clear in AWS documentation:

http://docs.aws.amazon.com/AmazonVPC/latest/UserGuide/VPCDHCPOptions.html#DHCPOptions

After you create a set of DHCP options, you can't modify them. If you want your VPC to use a different set of DHCP options, you must create a new set and associate them with your VPC. You can also set up your VPC to use no DHCP options at all.

You can have multiple sets of DHCP options, but you can associate only one set of DHCP options with a VPC at a time. If you delete a VPC, the DHCP options set associated with the VPC are also deleted.

You can highlight the text above to change formatting and highlight code.

```


----------------------------------------




## 資源
-- [Security Best Practice whitepaper](https://d0.awsstatic.com/whitepapers/Security/AWS_Security_Best_Practices.pdf)
-- [Intro_to_AWS_Security](https://d0.awsstatic.com/whitepapers/Security/Intro_to_AWS_Security.pdf)
