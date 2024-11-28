# Two-Tier-Architecture-Using-AWS
In this project I will deploy a two tier architecture using terraform for AWS. The two tier architecture will consist of two layers; Client and Database layers. Terraform is unique in the respect of its open world and agnostic meaning multiple cloud providers can be used. 


![image](https://github.com/user-attachments/assets/f7820a5e-f6f4-48c9-8fa5-493be3860fd9)



Benefits of Two Tier Architecture


Scalability - Fault Tolerance  - Security - Performance













This Two tier architecture will consist of;
•	VPC with a CIDR range of 0.0.0.0/16
•	Two public subnets and two private subnets in two Availability zones.
•	Deploy an RDS instance
•	An Application Load Balancer (ALB) will direct traffic to the subnets
•	Deploy one EC2 in each subnet
•	Internet gateway and Elastic Ips for the EC2 instances.



                                                                    Step one






The first part of this project is to establish which provider I want to use (AWS) and to set up my network_resources.tf file, this is essential as all of my code will be saved here allowing me to connect to the AWS console and manage the services.
This file will contain; VPC, Subnets, Internet Gateway, Route Table, Load Balancers.

First step is to create the VPC and public and private subnets.




![image](https://github.com/user-attachments/assets/3b1908f7-77ca-49f1-bcf6-720efb12d377)![image](https://github.com/user-attachments/assets/69ec4972-003b-49dd-836e-5a875c1581eb)






The route table and Internet Gateway are created also, the route table association is compiled with a cidr range 0.0.0.0/0


![image](https://github.com/user-attachments/assets/a3498583-99c6-4ac2-9f74-33eda245de61)


One of the final inputs in this file is the Load balancer and creating the target groups using port 80 HTTP



![image](https://github.com/user-attachments/assets/f9dcba15-2b41-4755-b27c-7a3a195b70b0)




                                                                       Step two

The next step in this project is creating the security _resources.tf . This is file will contain the security measurements for the application such as defining the security groups for the EC2 and Load Balancers.
Ports used were 80 and 22 with the same cidr range as before 0.0.0.0/0




                                                                       Step Three
The next file I will create is the EC2-resources.tf  - this will contain the resources responsible for provisioning EC2 instances, this example will include two EC2 instances both with NGINX web server installed. 
Two Elastic Ips will be created, one for each instance.

Firstly, I crated EC2 instance titled ‘two-tier-web-server’ I used a T2 micro due to its free tier eligibility I also copied over the AMI while also installing NGINX – I repeated this step again for my second EC2 instance. The instance that I used was Amazon Linux.



![image](https://github.com/user-attachments/assets/3f74a253-0ab5-4d5b-99b4-48b470a812ba)




Last part of this file; creating Elastic IP. 



![image](https://github.com/user-attachments/assets/2e5f0ed0-929a-425f-aa59-09dd29bf4094)



                                                                 Step Four

This is last stage I created the file db-resources.tf. This file is used to configure the RDS database, it is crucial this file is set up with correct configurations, storage and backup settings. 
The instance class used was 'db.t3.micro' - I also configured the the database to have a backup between 22:00-23:00


![image](https://github.com/user-attachments/assets/3682c1aa-d952-49fa-a8c4-1b2654065e3e)






























