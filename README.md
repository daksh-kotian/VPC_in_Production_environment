# VPC in Production Environment

This possible demonstration outlines the steps involved in creating a Virtual Private Cloud (VPC), which may then be used to house servers in a setting that is focused on production.

A deployment method is used, in which servers are spread across two different Availability Zones, to improve operational robustness. An Auto Scaling group is used in conjunction with an Application Load Balancer to accomplish this distribution. By positioning the servers inside private subnets, a security safeguard is additionally put in place. The aforementioned load balancer is used to redirect requests made to the servers. A Network Address Translation (NAT) gateway is also used to connect the servers to the internet, and it is deployed in both of the selected availability zones to further increase system resilience.


## Implementation

Architecture : 

![App Screenshot](https://github.com/asthasharma1712/VPC_in_Production_Environment/assets/85539636/03e5432e-71cc-4453-9fc0-82c21ed945e1)


Step 1 : Create the VPC

Use the following procedure to create a VPC with a public subnet and a private subnet in two Availability Zones, and a NAT gateway in each Availability Zone.

    1.1 - Configure the VPC
        : Select VPC and more
        : For Name tag auto-generation, enter a name for the VPC.
        : For IPv4 CIDR block, you can keep the default suggestion, or alternatively you can enter the CIDR block required by your application or network.

    1.2 - Configure the AZs, public and private subnets, NAT gateway and VPC endpoints as mentioned below
              
![App Screenshot](https://github.com/asthasharma1712/VPC_in_Production_Environment/assets/85539636/a1c7cb42-f9f6-422c-bf22-a17efc565ec4)


Preview : 
![App Screenshot](https://github.com/asthasharma1712/VPC_in_Production_Environment/assets/85539636/78ef1d15-7e84-485c-a046-ebef0d1b7bdf)


Step 2 : To launch instances by using an Auto Scaling group

![App Screenshot](https://github.com/asthasharma1712/VPC_in_Production_Environment/assets/85539636/8c27eca8-fd1c-406e-8605-7163ae1d5f49)

    
    2.1 - Create a launch template to specify the configuration information needed to launch your EC2 instances by using Amazon EC2 Auto Scaling.
          Note : Use same key pair (login) for the entire  project.         
Refer [Create a launch template for your Auto Scaling group](https://docs.aws.amazon.com/autoscaling/ec2/userguide/create-launch-template.html) in the Amazon EC2 Auto Scaling User Guide. 

  
    2.2 - Create an Auto Scaling group, which is a collection of EC2 instances with a minimum, maximum, and desired size.
 Refer [Create an Auto Scaling group using a launch template](https://docs.aws.amazon.com/autoscaling/ec2/userguide/create-asg-launch-template.html) in the Amazon EC2 Auto Scaling User Guide.
    
    2.3 - Create a load balancer, which distributes traffic evenly across the instances in your Auto Scaling group, and attach the load balancer to your Auto Scaling group.
For more information, see the [Elastic Load Balancing User Guide](https://docs.aws.amazon.com/elasticloadbalancing/latest/userguide/what-is-load-balancing.html) and [Use Elastic Load Balancing](https://docs.aws.amazon.com/autoscaling/ec2/userguide/autoscaling-load-balancer.html) in the Amazon EC2 Auto Scaling User Guide.

Step 3 : Create Bastion Host

A server called a "bastion host" is used to grant access to a private subnet from an external network, such the Internet, Public subnet. A bastion host must reduce the likelihood of infiltration because of its vulnerability to possible attack. To reduce the risk of enabling SSH connections from an external network to Linux instances created in a private subnet of your Amazon Virtual Private Cloud (VPC), for instance, you can use a bastion host.

Refer [Configuring private network access using a Linux Bastion Host](https://docs.aws.amazon.com/mwaa/latest/userguide/tutorials-private-network-bastion.html)


Step 4 : Run the following commands in terminal

    [1] scp -i localmachine/path_to_the_file username@server_ip:/path_to_remote_director

    [2] ssh -i pemfile.pem ubuntu@public_ip_of_bastion

    [3] ssh -i pemfile.pem ubuntu@public_ip_of_other_instance

    [4] vim index.html
        Note : Add html code for your webpage and save using :wq command
    
    [5] python3 -m http.server 80

Step 5 : Create an Application Load Balancer

![App Screenshot](https://github.com/asthasharma1712/VPC_in_Production_Environment/assets/85539636/aedd8792-a9df-4858-89fe-dbe833f45b32)

Refer [Create application Load Balancers through the AWS Management Console](https://docs.aws.amazon.com/elasticloadbalancing/latest/application/application-load-balancer-getting-started.html)
    
    Note : Set target group at port 80 (http)

Step 6 : Copy DNS Name from load balancer created to a new tab to view your webpage.

Now, you can see your webpage successfully hosted !!



  


## References

 - [Example: VPC with servers in private subnets and NAT](https://docs.aws.amazon.com/vpc/latest/userguide/vpc-example-private-subnets-nat.html)
 -  [Create a launch template for your Auto Scaling group](https://docs.aws.amazon.com/autoscaling/ec2/userguide/create-launch-template.html) in the Amazon EC2 Auto Scaling User Guide.
 -  [Create an Auto Scaling group using a launch template](https://docs.aws.amazon.com/autoscaling/ec2/userguide/create-asg-launch-template.html) 
 - [Elastic Load Balancing User Guide](https://docs.aws.amazon.com/elasticloadbalancing/latest/userguide/what-is-load-balancing.html) and [Use Elastic Load Balancing](https://docs.aws.amazon.com/autoscaling/ec2/userguide/autoscaling-load-balancer.html) in the Amazon EC2 Auto Scaling User Guide.
 - [Configuring private network access using a Linux Bastion Host](https://docs.aws.amazon.com/mwaa/latest/userguide/tutorials-private-network-bastion.html)
- [Create application Load Balancers through the AWS Management Console](https://docs.aws.amazon.com/elasticloadbalancing/latest/application/application-load-balancer-getting-started.html)
