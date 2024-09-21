# CloudFormation Templates README

## Overview
This CloudFormation templates to create the necessary infrastructure for deploying a web application, 
The templates include configurations for a Virtual Private Cloud (VPC), EC2 instance, Relational Database Service (RDS), and Elastic IP (EIP).

## Infrastructure Components
The infrastructure is created using the following CloudFormation templates:

1. **vpc.yaml**: This template creates a Virtual Private Cloud (VPC) with public and private subnets, an Internet Gateway, routing tables, and security groups.

2. **ec2.yaml**: This template creates an Amazon EC2 instance in the public subnet, installs Apache HTTP Server, PHP, and MariaDB, and downloads the web application code from a GitHub repository.

3. **eip.yaml**: This template allocates an Elastic IP address and associates it with the EC2 instance created in the `ec2.yaml` template.

4. **rds.yaml**: This template creates an Amazon Relational Database Service (RDS) instance in the private subnets, configured with a MySQL database.

## Getting Started
## Deployment
1. Sign in to the AWS Management Console and navigate to the CloudFormation service.

2. Click "Create stack" and select "With new resources (standard)".

3. Under "Specify template", select "Upload a template file" and upload the `vpc.yaml` template file and click "Next".

4. Set the desired values for the VPC, subnet, and SSH CIDR parameters, and click "Next" until you reach the "Review" page.

5. Review the details and click "Create stack" to create the VPC stack.

6. Once the VPC stack is created, repeat steps 2-5 with the `ec2.yaml` template file. When prompted for parameters, enter the name of the VPC stack you just created in the "VpcStackName" parameter.

7. Create the Elastic IP stack by repeating the process with the eip.yaml template file. When prompted for parameters, enter the name of the EC2 stack you created in the "Ec2StackName" parameter.

8. Repeat the process again with the rds.yaml template file, providing the VPC stack name in the "VpcStackName" parameter. After that, connected to the EC2 instance, you need to modify the database PHP file to connect to the hosted RDS database. Navigate to the directory where your PHP application files are located ( /var/www/html/) and open the database PHP file in a text editor using nano. Then, replace the existing values with the details from your RDS instance and save the changes.

9. After all the stacks have been created successfully, navigate to the Outputs tab of the Elastic IP stack to retrieve the allocated Elastic IP address. Use this IP address to access the web application in your browser.

## Cleanup
To delete the infrastructure and application, follow these steps:

1. In the CloudFormation console, select the Elastic IP stack and click "Delete".
2. Once the Elastic IP stack is deleted, repeat the process for delete RDS stack.
3. Then, delete the EC2 stack and followed by delete the VPC stack.
