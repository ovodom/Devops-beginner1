# AWS VPC Project

**INTRODUCTION:**

A VPC (Virtual Private Cloud) in AWS (Amazon Web Services) is a service that lets you start AWS resources in a wise isolated virtual network that you define. Below is a couple of components and features of an AWS VPC:
1.	Subnets
2.	IP addresses 
3.	Route Tables
4.	Internet Gateway
5.	NAT Gateway and NAT Instances 
6.	Security Groups
7.	Network ACLs
8.	VPC Peering
9.	VPN Gateway
10.	VPC Endpoints
11.	AWS Direct Connect.



**DYNAMICS:**

**Step 1**

Create a VPC for project and assign attach an internet gateway to it.

•	Login to your AWS management console and search VPC 



![1](img/img1.png)



![1](img/img2.png)



![1](img/img3.png)




•	create an Internet Gateway




![1](img/img4.png)



•	Attach Internet Gateway to VPC



![1](img/img5%20(2).png)




![1](img/img6.png)




**Step 2**



•	Create The Public Subnet



![2](img/img7.png)



![2](img/img9.png)



![2](img/img10.png)



![2](img/img11.png)



![2](img/img12.png)




•	Create The Private Subnets following the same steps taken for the creation of the public subnet also having subnets for 2b and 2c:



![2](img/img13.png)



•	Create for Database, Management and Platform (Note: These are Private)



![2](img/img14.png)



You will have something like this,




![2](img/img15.png)



**Step 3**


Route Table Design

•	Create Public Route Table and their subnet association.



![3](img/img16.png)



![3](img/img17.png)



![3](img/img18.png)



![3](img/img19.png)



•	Create Private Route Table (Application, Database, Management and Platform)



![3](img/img20.png)



![3](img/img21.png)



![3](img/img22.png)




![3](img/img23.png)




![3](img/img24.png)




![3](img/img25.png)




**Step 4**

NAT Gateway



![4](img/img26.png)



•	Select a Subnet and allocate an IP address



![4](img/img27.png)




![4](img/img28.png)




**Step 5**


Adding the NAT Gateway to the Route Tables one after the other



![5](img/img29.png)



•	add route to each Route Table 



![5](img/img30.png)



![5](img/img31.png)




![5](img/img32.png)



•	Notice the status of the NAT gateway is active



![5](img/img33.png)




•	add route for Route Table (public)

![5](img/img34.png)



![5](img/img35.png)




**Step 6**

AWS VPC Topology



![6](img/img36.png)



![6](img/img37.png)



![6](img/img38.png)



**Step 7**


Network ACLs

![7](img/img39.png)



![7](img/img40.png)




DB NACL (Inbound Rules)

![7](img/img41.png)



![7](img/img42.png)



![7](img/img44a.png)




![7](img/img45.png)




DB NACL (Outbound Rules)


![7](img/img43.png)



![7](img/img44.png)




![7](img/img46.png)




![7](img/img47.png)

 




