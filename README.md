

# AWS_sysops_resource


for AWS Certified Sysops - Associate exam


## 官方範例


## 有用的範例問題
```
You want to pass queue messages that are 1GB each. How should you achieve this?
A) Use Kinesis as a buffer stream for message bodies. Store the checkpoint id for the placement in the Kinesis Stream in SQS.
B) Use the Amazon SQS Extended Client Library for Java and Amazon S3 as a storage mechanism for message bodies.
C) Use SQS’s support for message partitioning and multi-part uploads on Amazon S3.
D) Use AWS EFS as a shared pool storage medium. Store filesystem pointers to the files on disk in the SQS message bodies.
```
> B

 (Amazon SQS messages with Amazon S3 can be useful for storing and retrieving messages with a message size of up to 2 GB. To manage Amazon SQS messages with Amazon S3, use the Amazon SQS Extended Client Library for Java. Refer link)

-- [Link](http://docs.aws.amazon.com/AWSSimpleQueueService/latest/SQSDeveloperGuide/sqs-s3-messages.html)


-----------------------------------------------

```
Company ABCD has recently launched an online commerce site for bicycles on AWS. They have a “Product” DynamoDB table that stores details for each bicycle, such as, manufacturer, color, price, quantity and size to display in the online store. Due to customer demand, they want to include an image for each bicycle along with the existing details. Which approach below provides the least impact to provisioned throughput on the “Product” table?
A) Serialize the image and store it in multiple DynamoDB tables
B) Create an “Images” DynamoDB table to store the Image with a foreign key constraint to the “Product” table
C) Add an image data type to the “Product” table to store the images in binary format
D) Store the images in Amazon S3 and add an S3 URL pointer to the “Product” table item for each image
```
> D


----------------------------------------------


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
An organization has established an Internet-based VPN connection between their on-premises data center and AWS. They are considering migrating from VPN to AWS DirectConnect.

Which operational concern should drive an organization to consider switching from an Internet-based VPN connection to AWS DirectConnect?

A. AWS DirectConnect provides greater redundancy than an Internet-based VPN connection.

B. AWS DirectConnect provides greater resiliency than an Internet-based VPN connection.

C. AWS DirectConnect provides greater bandwidth than an Internet-based VPN connection.

D. AWS DirectConnect provides greater control of network provider selection than an Internet-based VPN connection.
```
> C

In particular, the Direct Connect Overview and Service Highlights seem to support your conclusion that the correct response is C:


"Direct Connect... can reduce your network costs, increase bandwidth throughput, and provide a more consistent network experience than Internet-based connections."


問：使用 AWS Direct Connect 和私有網路連接有什麼好處？


在許多情況下，私有網路連接可以降低成本、提高頻寬，還有提供比網際網路連接更為一致的網路體驗。


----------------------------------


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

http://docs.aws.amazon.com/AmazonVPC/latest/UserGuide/VPCDHCPOptions.html

http://docs.aws.amazon.com/AmazonVPC/latest/UserGuide/vpc-dns.html

```


----------------------------------------


## 官方範例

```
When working with Amazon RDS, by default AWS is responsible for implementing which two management-related activities? (Pick 2 correct answers)

A. Importing data and optimizing queries
B. Installing and periodically patching the database software
C. Creating and maintaining automated database backups with a point-in-time recovery of up to five minutes
D. Creating and maintaining automated database backups in compliance with regulatory long-term retention requirements
```
> B & C

```
Amazon RDS gives you online access to the capabilities of a MySQL, Oracle, Microsoft SQL Server, PostgreSQL, or Amazon Aurora relational database management system. This means that the code, applications, and tools you already use today with your existing databases can be used with Amazon RDS. Amazon RDS automatically patches the database software and backs up your database, storing the backups for a user-defined retention period and enabling point-in-time recovery. You benefit from the flexibility of being able to scale the compute resources or storage capacity associated with your Database Instance (DB Instance) via a single API call.
```


----------------------------------


```
You maintain an application on AWS to provide development and test platforms for your developers. Currently both environments consist of an m1.small EC2 instance. Your developers notice performance degradation as they increase network load in the test environment.


How would you mitigate these performance issues in the test environment?

A. Upgrade the m1.small to a larger instance type
B. Add an additional ENI to the test instance
C. Use the EBS optimized option to offload EBS traffic
D. Configure Amazon Cloudwatch to provision more network bandwidth when network utilization exceeds 80%
```
> A

```
An Elastic IP address (EIP) is a static IP address designed for dynamic cloud computing. With an EIP, you can mask the failure of an instance or software by rapidly remapping the address to another instance in your account. It won’t help us so (B) is out
Only the larger instance types support the EBS optimized option, so (C) cannot be the answer.
Cloudwatch can monitor the bandwidth however I am almost certain that it cannot provision more bandwidth, so (D) cannot be the answer.
So the answer is (A). If we upgrade the instance it will be able to cope with the increase in load hopefully.
```


---------------------------


```
Per the AWS Acceptable Use Policy, penetration testing of EC2 instances:

A. may be performed by the customer against their own instances, only if performed from EC2 instances
B. may be performed by AWS, and is periodically performed by AWS.
C. may be performed by AWS, and will be performed by AWS upon customer request.
D. are expressly prohibited under all circumstances.
E. may be performed by the customer against their own instances with prior authorization from AWS.
```
> E

```
Permission is required for all penetration tests.
To request permission, you must be logged into the AWS portal using the credentials associated with the instances you wish to test, otherwise the form will not pre-populate correctly. If you have hired a third party to conduct your testing, AWS suggest that you complete the form and then notify your third party when they grant approval.
At this time, the AWS policy does not permit testing m1.small or t1.micro instance types. This is to prevent potential adverse performance impacts on the resources you may be sharing with other customers in a multi-tenant environment.
The information you share with AWS as part of this process is kept confidential within AWS. It will not be shared with third parties without your permission.
```


------------------------------------------

```
You have been tasked with identifying an appropriate storage solution for a NoSQL database that requires random I/O reads of greater than 100,000 4kB IOPS.

Which EC2 option will meet this requirement?

A. EBS provisioned IOPS
B. SSD instance store
C. EBS optimized instances
D. High Storage instance configured in RAID 10
```
> D

```
I do not think that AWS offers a single disk solution that provides I/O reads of greater than 100,000 4kB IOPS.
Consequently the only possible answer is (D)
```


------------------------------------

```
Instance A and instance B are running in two different subnets A and B of a VPC. Instance A is not able to ping instance B.

What are two possible reasons for this? (Pick 2 correct answers)

A. The routing table of subnet A has no target route to subnet B
B. The security group attached to instance B does not allow inbound ICMP traffic
C. The policy linked to the IAM role on instance A is not configured correctly
D. The NACL on subnet B does not allow outbound ICMP traffic
```
> B & D

```
(A) Is incorrect because you can’t modify the routing table for intra-VPC communication. Intra-VPC routes are always local and therefore this route is always valid.

(C) Is incorrect because IAM doesn’t directly control what your resources can access.

The fact that ping uses ICMP would also seem to suggest that the only possible answers are (B) and (D)
```


--------------------------------

```
Your web site is hosted on 10 EC2 instances in 5 regions around the globe with 2 instances per region. How could you configure your site to maintain site availability with minimum downtime if one of the 5 regions was to lose network connectivity for an extended period of time?

A. Create an Elastic Load Balancer to place in front of the EC2 instances. Set an appropriate health check on each ELB.
B. Establish VPN Connections between the instances in each region. Rely on BGP to failover in the case of a region wide connectivity outage
C. Create a Route 53 Latency Based Routing Record Set that resolves to an Elastic Load Balancer in each region. Set an appropriate health check on each ELB.
D. Create a Route 53 Latency Based Routing Record Set that resolves to Elastic Load Balancers in each region and has the Evaluate Target Health flag set to true.
```
> D

```
Your set up is as follows.

1. You have multiple zones
2. You have multiple ELB’s. One per region
3. Route 53 can check the health of the target Load Balancer

Configure route 53 to distribute traffic based on latency and to check the target health. If for some reason a region  goes down, route 53 would stop sending traffic to the unavailable region and route it to the next closest region.
```


------------------------------------

```
You run a stateless web application with the following components: Elastic Load Balancer (ELB), 3 Web/Application servers on EC2, and 1 MySQL RDS database with 5000 Provisioned IOPS. Average response time for users is increasing. Looking at CloudWatch, you observe 95% CPU usage on the Web/Application servers and 20% CPU usage on the database. The average number of database disk operations varies between 2000 and 2500.

Which two options could improve response times? (Pick 2 correct answers)

A. Choose a different EC2 instance type for the Web/Application servers with a more appropriate CPU/memory ratio
B. Use Auto Scaling to add additional Web/Application servers based on a CPU load threshold
C. Increase the number of open TCP connections allowed per web/application EC2 instance
D. Use Auto Scaling to add additional Web/Application servers based on a memory usage threshold
```
> A & B

明顯缺CPU


---------------------------------------

```
Which features can be used to restrict access to data in S3? (Pick 2 correct answers)

A. Create a CloudFront distribution for the bucket.
B. Set an S3 bucket policy.
C. Use S3 Virtual Hosting.
D. Set an S3 ACL on the bucket or the object.
E. Enable IAM Identity Federation.
```
> B & D

```
Customers may use four mechanisms for controlling access to Amazon S3 resources:

Identity and Access Management (IAM) policies.
Bucket policies.
Access Control Lists (ACLs).
Query string authentication.
IAM enables organizations with multiple employees to create and manage multiple users under a single AWS account. With IAM policies, companies can grant IAM users fine-grained control to their Amazon S3 bucket or objects while also retaining full control over everything the users do. With bucket policies, companies can define rules which apply broadly across all requests to their Amazon S3 resources, such as granting write privileges to a subset of Amazon S3 resources. Customers can also restrict access based on an aspect of the request, such as HTTP referrer and IP address. With ACLs, customers can grant specific permissions (i.e. READ, WRITE, FULL_CONTROL) to specific users for an individual bucket or object. With query string authentication, customers can create a URL to an Amazon S3 object which is only valid for a limited time.
```


-------------------------------------

```
You need to establish a backup and archiving strategy for your company using AWS. Documents should be immediately accessible for 3 months and available for 5 years for compliance reasons.

Which AWS service fulfills these requirements in the most cost effective way?

A. Use StorageGateway to store data to S3 and use life-cycle policies to move the data into Redshift for long-time archiving
B. Use DirectConnect to upload data to S3 and use IAM policies to move the data into Glacier for longtime archiving
C. Upload the data on EBS, use life-cycle policies to move EBS snapshots into S3 and later into Glacier for long-time archiving
D. Upload data to S3 and use life-cycle policies to move the data into Glacier for long-time archiving.
```
> D

```
The best way for the document to be immediately accessible is to upload the data to S3. Amazon Simple Storage Service (Amazon S3) is storage for the Internet. You can use Amazon S3 to store and retrieve any amount of data at any time, from anywhere on the web.
So how do you move your data from Amazon S3 to Glacier? Using Lifecycle Policies. These policies are basically just rules that you can setup to move the data from S3 to Glacier at specific times.
Using lifecycle configuration, you can transition objects to the GLACIER storage class—that is, archive data to Amazon Glacier, a lower-cost storage solution.
```


-----------------------------------------------

```
Given the following IAM policy:

{
"Version": "2012-10-17",
 "Statement":
 [
 { "Effect": "Allow",
 "Action": [
 "s3:Get*", "s3:List*"
 ],
 "Resource": "*"
 },
 {
 "Effect": "Allow",
 "Action": "s3:PutObject",
"Resource": "arn:aws:s3:::corporate_bucket/*"
 }
 ]
}

What does the IAM policy allow? (Pick 3 correct answers)

A. The user is allowed to read objects from all S3 buckets owned by the account
B. The user is allowed to write objects into the bucket named ‘corporate_bucket’
C. The user is allowed to change access rights for the bucket named ‘corporate_bucket’
D. The user is allowed to read objects in the bucket named ‘corporate_bucket’ but not allowed to list the objects in the bucket
E. The user is allowed to read objects from the bucket named ‘corporate_bucket’
```
> A B E

```
"Effect": "Allow",
 "Action": [
 "s3:Get*", "s3:List*"
The user is allowed to read objects from all S3 buckets owned by the account.(A)
He can also list objects from all S3 buckets owned by the account.Therefore (D) cannot be correct.
If he can read all buckets then he can read objects from the bucket named ‘corporate_bucket'(E)
```


------------------------------------

## 資源
 - [Security Best Practice whitepaper](https://d0.awsstatic.com/whitepapers/Security/AWS_Security_Best_Practices.pdf)
 - [Intro_to_AWS_Security](https://d0.awsstatic.com/whitepapers/Security/Intro_to_AWS_Security.pdf)
