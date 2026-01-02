<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Creating a Private Subnet

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-networks-private)

**Author:** Cody Chinothai  
**Email:** cchinothai@gmail.com

---

## Creating a Private Subnet

![Image](http://learn.nextwork.org/enthusiastic_turquoise_radiant_monstera_deliciosa/uploads/aws-networks-private_afe1fdbd)

---

## Introducing Today's Project!

### What is Amazon VPC?

Amazon VPC is your own delegated space within the AWS Cloud that lets you control all network configurations for that space. 

### How I used Amazon VPC in this project

In today's project, I used Amazon VPC to create a private subnet, route table, and network ACL alongside our public subnets.

### One thing I didn't expect in this project was...

One thing to take into consideration is that your CIDR ranges for the private subnet must not overlap with that of the other subnets in your VPC. Ensure your VPC CIDR ranges allow space for separate channels. 

### This project took me...

---------

---

## Private vs Public Subnets

Public subnets will have traffic flow that exit the subnet to the internet gateway. Private subnets restrict this capability to keep all accessibility in house within the VPC. 

Having private subnets are useful because they allow control of confidential resources that you don't want users to see. 

My private and public subnets cannot have the same CIDR ranges as that would cause merging traffic. We make sure that our VPC was set as /16 so that we can have traffic channels where each subnet has an address range from 0 to 255. 

![Image](http://learn.nextwork.org/enthusiastic_turquoise_radiant_monstera_deliciosa/uploads/aws-networks-private_afe1fdbd)

---

## A dedicated route table

By default, my private subnet is associated with the default route table that was created for my public subnets. We want a separate route table for our private cases. 

I had to set up a new route table because our prior route tables defined traffic for our internet gateway. However, we will not use this internet gateway in a private subnet, so we need to create a separate route table.

My private subnet's dedicated route table only has one inbound and one outbound rule that allows local traffic within the subnet. 

![Image](http://learn.nextwork.org/enthusiastic_turquoise_radiant_monstera_deliciosa/uploads/aws-networks-private_b4b904b5)

---

## A new network ACL

By default, my private subnet is associated with our default NACL associated with our VPC. This is because we  haven't made an explicit association yet. 

I set up a dedicated network ACL for my private subnet because we want to implement traffic security beyond our private route table that excludes connection to our internet gateway. We are vulnerable to additional threats if any part of our VPC becomes compromised, so the NACL is an extra means of protection. 

My new network ACL has two simple rules - deny all inbound and outbound traffic. 

![Image](http://learn.nextwork.org/enthusiastic_turquoise_radiant_monstera_deliciosa/uploads/aws-networks-private_1ed2cb07)

---

---
