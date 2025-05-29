<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Creating a Private Subnet

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-networks-private)

**Author:** Albert  
**Email:** tapcyberx@gmail.com

---

## Creating a Private Subnet

![Image](http://learn.nextwork.org/delighted_indigo_timid_orc/uploads/aws-networks-private_afe1fdbd)

---

## Introducing Today's Project!

### What is Amazon VPC?

Amazon VPC is a service that allows you to create a virtual network within the AWS cloud, giving you control over your network environment. it useful for isolating your AWS resources, defining network configurations, and managing security policies.

### How I used Amazon VPC in this project

In today's project I created a new subnet and set its CIDR block to avoid an overlap with your public subnet.
I also made this subnet private by assigning it to a dedicated route table that doesn't route traffic to an internet gateway and Then, I set up custom network ACLs to control inbound and outbound traffic for this private subnet - denying all traffic by default.

### One thing I didn't expect in this project was...

I didn't expect errors but as always I  think is the best way to learn.

### This project took me...

This project took me around 2h to completed.

---

## Private vs Public Subnets

The main difference is internet accessibility: A public subnet is connected to the internet through an internet gateway, which allows resources like EC2 instances to send and receive traffic from the internet.
A private subnet, on the other hand, has no direct internet access it’s typically used for internal resources like databases or backend services that shouldn’t be publicly exposed.

This separation helps improve security and network architecture within your VPC.



Having private subnets are useful because you can keep resources in private. For example databases and customer information.

My private and public subnets cannot have the same IPv4 VPC CIDR block i.e the same range of IP addresses. The CIDR block for every subnet must be unique and cannot overlap with another subnet.

![Image](http://learn.nextwork.org/delighted_indigo_timid_orc/uploads/aws-networks-private_afe1fdbd)

---

## A dedicated route table

By default, my private subnet is associated with the default route table i.e. a route table that has a route to an internet gateway.

I had to set up a new route table because my subnet can't have a route to an internet gateaway.

My private subnet's dedicated route table only has one inbound and one outbound rule that allows internal communication i.e. with a dentination of another resource within my VPC.

![Image](http://learn.nextwork.org/delighted_indigo_timid_orc/uploads/aws-networks-private_b4b904b5)

---

## A new network ACL

By default, my private subnet is associated with the default network ACL that's set up for every VPC created in my AWS account.

I set up a dedicated network ACL for my private subnet to add an extra layer of security. While the private subnet is already isolated from the internet by not having a route to an internet gateway, configuring a specific network ACL helps control internal traffic more precisely.

This becomes especially important in scenarios where a security breach occurs in the public subnet. If the network ACL allows unrestricted inbound or outbound traffic, compromised traffic could potentially reach private resources. By setting custom rules, I can limit access and reduce the risk of lateral movement between subnets.

My new network ACL has two simple rules - deny all inbound and deny all the outbound traffic.

![Image](http://learn.nextwork.org/delighted_indigo_timid_orc/uploads/aws-networks-private_1ed2cb07)

---

---
