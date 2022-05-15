# Move-EC2-Instance-to-a-Different-Availability-Zone-Virtual-Private-Cloud-or-a-Region

## What is EC2
Amazon Elastic Compute Cloud (Amazon EC2) provides scalable computing capacity in the Amazon Web Services (AWS) Cloud. Using Amazon EC2 eliminates your need to invest in hardware up front, so you can develop and deploy applications faster. You can use Amazon EC2 to launch as many or as few virtual servers as you need, configure security and networking, and manage storage. Amazon EC2 enables you to scale up or down to handle changes in requirements or spikes in popularity, reducing your need to forecast traffic. (IaaS)
- Refer to this link:-https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/concepts.html

## VPC
Amazon Virtual Private Cloud (Amazon VPC) enables you to launch AWS resources into a virtual network that you've defined. This virtual network closely resembles a traditional network that you'd operate in your own data center, with the benefits of using the scalable infrastructure of AWS.
- Refer to this link:- https://docs.aws.amazon.com/vpc/latest/userguide/what-is-amazon-vpc.html

## Regions, Availability Zones, and Local Zones
Amazon cloud computing resources are hosted in multiple locations world-wide. These locations are composed of AWS Regions, Availability Zones, and Local Zones. Each AWS Region is a separate geographic area. Each AWS Region has multiple, isolated locations known as Availability Zones.
- Refer to this link:- https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Concepts.RegionsAndAvailabilityZones.html

## Whats the purpose to move resources one region to another region 
Disaster recovery strategies available to you within AWS can be broadly categorized into four approaches, ranging from the low cost and low complexity of making backups to more complex strategies using multiple active Regions. Active/passive strategies use an active site (such as an AWS Region) to host the workload and serve traffic. The passive site (such as a different AWS Region) is used for recovery. The passive site does not actively serve traffic until a failover event is triggered.
- Refer to this link:- https://docs.aws.amazon.com/whitepapers/latest/disaster-recovery-workloads-on-aws/disaster-recovery-options-in-the-cloud.html

## Backup and restore
Backup and restore is a suitable approach for mitigating against data loss or corruption. This approach can also be used to mitigate against a regional disaster by replicating data to other AWS Regions, or to mitigate lack of redundancy for workloads deployed to a single Availability Zone. 

## Steps to be followed:- 

## Step1 Create a VPC in ap-south-1 (Mumbai) region 
![image](https://user-images.githubusercontent.com/63963025/168437759-54108b51-9093-44b7-ad39-15d29ac3aa69.png)

- Create a VPC 
![image](https://user-images.githubusercontent.com/63963025/168438519-5db42966-b34a-4bfe-8ffd-6a0e52129fb5.png)

- Confingure VPC with CIDR range <b>10.0.0.0/24</b> create VPC 
![image](https://user-images.githubusercontent.com/63963025/168438803-1e33d6d0-4384-4393-b015-2ffd55b9a59a.png)

- Create subnet filter vpc (mumbai-vpc)
![image](https://user-images.githubusercontent.com/63963025/168439238-49e140f1-17a5-4dfd-a4aa-92b08b3bf54d.png)

- Select CIDR range <b>10.0.0.0/28</b>
![image](https://user-images.githubusercontent.com/63963025/168439364-eb13b0c3-94a3-409f-881c-f61d605d03da.png)

- Create IGW (Internet Gateway) and attach to Mumbai VPC
 ![image](https://user-images.githubusercontent.com/63963025/168439465-4e5b8ced-7f48-43a6-85bd-a9d0b3c6b65b.png)
 ![image](https://user-images.githubusercontent.com/63963025/168439489-7c88aeb2-eb04-4125-bbd6-cedc5a4e5fb0.png)

- Configure Route table 
![image](https://user-images.githubusercontent.com/63963025/168441127-8c1ddd56-eba2-44b5-91d1-0543621c3a6c.png)

- Lets create another VPC in different region here iam using eu-west-1 (ireland) you can use different region as you wish 
![image](https://user-images.githubusercontent.com/63963025/168439736-99a606f7-ef15-41ed-977e-27bf88ad2ca9.png)

## Step 2 Create a VPC in eu-west-1 (ireland) region
- Create VPC
 ![image](https://user-images.githubusercontent.com/63963025/168439963-b5ed74e3-d5dc-4a69-bfbf-46f64b29e210.png)

- Create subnet
![image](https://user-images.githubusercontent.com/63963025/168440046-0dc9259c-3690-41ba-bc64-b7ea03f66c2d.png)

- IGW (ireland-igw)
![image](https://user-images.githubusercontent.com/63963025/168440075-d1065c25-dcbb-440f-8c28-253c3e172836.png)

- select IGW and go to Action --> Attach vpc --> ireland-vpc

- Configure route table for ireland region 
![image](https://user-images.githubusercontent.com/63963025/168442085-ad468a57-15a0-4bd9-95de-0949e6e1d619.png)
 
- Go back to mumbai region create  Virtaul machine EC2 
![image](https://user-images.githubusercontent.com/63963025/168440206-44ebda1a-549d-4891-97c5-e09f114d3f97.png)
![image](https://user-images.githubusercontent.com/63963025/168440340-8ada85dd-57af-4af1-a338-40c821387aea.png)

- Select OS 
 ![image](https://user-images.githubusercontent.com/63963025/168440359-0dd27d1c-8b71-4fd2-93d7-870c2a333472.png)
 
- instance type (t2 micro)
![image](https://user-images.githubusercontent.com/63963025/168440368-e3a708b6-c0d6-4d06-a126-ecf7fc3855a6.png)

- create key or select existing key 
![image](https://user-images.githubusercontent.com/63963025/168440401-2deea83a-a6db-4eca-945f-26d9619c8f69.png)

- In network select mumbai VPC and allow http and https Traffic 
![image](https://user-images.githubusercontent.com/63963025/168440876-8f2793ab-9db1-4153-8a5e-9ad03a47a5d6.png)

![image](https://user-images.githubusercontent.com/63963025/168440493-a0ec0f7a-3166-42c2-bf12-61fd5b7868af.png)

![image](https://user-images.githubusercontent.com/63963025/168440504-421a58e4-fe32-44a7-9034-8555c558142d.png)

- Storage Default 
- Advanced details --> User data 
![image](https://user-images.githubusercontent.com/63963025/168440605-7e62744a-ff56-4c1a-b262-3c5933943330.png)
- Its same as in GCP there is Metadata and inside that Metadata there is option call Startup-script 
```
#!/bin/bash
# Use this for your user data (script from top to bottom)
# install httpd (Linux 2 version)
yum update -y
yum install -y httpd
systemctl start httpd
systemctl enable httpd
echo "<h1>Hello Guys from $(hostname -f)</h1>" > /var/www/html/index.html
```
## User data
Specify user data to provide commands or a command script to run when you launch your instance.
- refer to this doc:-https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/user-data.html

- you should this kind of webapge 
![image](https://user-images.githubusercontent.com/63963025/168441279-cfbe35b4-e52b-4060-a5f9-4adca59797e4.png)

## Step3 Moving EC2 Intnace to another region

- Create an AMI (Amazon Machine Image) In GCP it is know as snapshot Right click there will be option call Image and template --> create image
![image](https://user-images.githubusercontent.com/63963025/168441554-1f200ca6-4643-4c63-83d2-3d8b89b698d5.png)

![image](https://user-images.githubusercontent.com/63963025/168441584-5a5423bb-fc79-4c22-9133-571c49805d25.png)

- Here the image is been created 
![image](https://user-images.githubusercontent.com/63963025/168441721-0f23aaf9-d40d-462f-80ea-e30e9ebe74fe.png)

- Now lets share this iamge to another region Right click --> Copy AMI option

![image](https://user-images.githubusercontent.com/63963025/168441749-551552c7-fd3d-45c3-8727-fddd86885958.png)

- Select region ireland or where you want to share the AMI 
![image](https://user-images.githubusercontent.com/63963025/168441788-0d69d8ca-9a29-48fc-9fc1-56e7e7b2211e.png)

![image](https://user-images.githubusercontent.com/63963025/168441825-19f2b781-0d12-4be3-a04c-7a3f46bd118a.png)

- Last step launch VM from that AMI 
![image](https://user-images.githubusercontent.com/63963025/168441901-d8b3cef1-9955-42af-a984-089ccaa9b2c2.png)

![image](https://user-images.githubusercontent.com/63963025/168441919-cfde7ac1-8b77-4478-ab06-f58ffd0641b4.png)

- create a new key for this region
- All default only change the VPC--> ireland-VPC--> Auto assign ip--> enable
![image](https://user-images.githubusercontent.com/63963025/168441988-a0754700-d9b8-4d0f-b987-a43a82201355.png)

- ssh to your webserver and start httpd 
![image](https://user-images.githubusercontent.com/63963025/168442365-6ce60e8e-caea-4746-8d5a-61832460a2e2.png)

- copy the external ip and paste in to your browser 
![image](https://user-images.githubusercontent.com/63963025/168442623-283f88c9-d039-4c08-9ec0-70d5bcd5abab.png)


- For eg anything happen in the region deu some natural disaster or if our machine fails or due to some reason we have to change our location to another region so we are using this AMI strategy
