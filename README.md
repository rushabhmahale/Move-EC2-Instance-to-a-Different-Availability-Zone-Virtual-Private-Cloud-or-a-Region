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

- Lets create another VPC in different region 
