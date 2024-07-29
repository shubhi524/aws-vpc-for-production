# aws-vpc-for-production
𝐃𝐞𝐬𝐢𝐠𝐧𝐢𝐧𝐠 𝐚 𝐒𝐞𝐜𝐮𝐫𝐞 𝐀𝐖𝐒 𝐕𝐏𝐂 𝐟𝐨𝐫 𝐏𝐫𝐨𝐝𝐮𝐜𝐭𝐢𝐨𝐧
𝐒𝐭𝐞𝐩 𝟏: 𝐂𝐫𝐞𝐚𝐭𝐞 𝐚 𝐕𝐏𝐂 𝐰𝐢𝐭𝐡 𝐓𝐰𝐨 𝐀𝐯𝐚𝐢𝐥𝐚𝐛𝐢𝐥𝐢𝐭𝐲 𝐙𝐨𝐧𝐞𝐬:

1. Log in to the AWS Management Console.

2. Navigate to the VPC Dashboard.

3. Click on “Your VPCs” and then click “Create VPC.”

4. Specify a name for your VPC, such as “ProductionVPC.”

5. Set the IPv4 CIDR block for your VPC. For example, use `10.0.0.0/16`.

6. Choose two different Availability Zones to enhance resiliency.

7. Create the VPC.

𝐒𝐭𝐞𝐩 𝟐: 𝐂𝐫𝐞𝐚𝐭𝐞 𝐏𝐫𝐢𝐯𝐚𝐭𝐞 𝐒𝐮𝐛𝐧𝐞𝐭𝐬:

1. In the VPC Dashboard, go to “Subnets.”

2. Click “Create Subnet.”

3. Select the VPC you just created.

4. Choose one of the Availability Zones.

5. Define the IPv4 CIDR block for the subnet, e.g., `10.0.1.0/24`.

6. Disable the “Auto-assign public IPv4 address” option to ensure the subnets are private.

7. Create the subnet.

8. Repeat the process to create a private subnet in the second Availability Zone.

𝐒𝐭𝐞𝐩 𝟑: 𝐒𝐞𝐭 𝐔𝐩 𝐚 𝐍𝐀𝐓 𝐆𝐚𝐭𝐞𝐰𝐚𝐲:

1. In the VPC Dashboard, go to “NAT Gateways.”

2. Click “Create NAT Gateway.”

3. Choose one of the private subnets and the corresponding Availability Zone.

4. Allocate an Elastic IP address if you haven’t already.

5. Create the NAT Gateway.

6. Repeat the process to create another NAT Gateway in the second Availability Zone.

𝐒𝐭𝐞𝐩 𝟒: 𝐂𝐨𝐧𝐟𝐢𝐠𝐮𝐫𝐞 𝐑𝐨𝐮𝐭𝐞 𝐓𝐚𝐛𝐥𝐞𝐬:

1. In the VPC Dashboard, navigate to “Route Tables.”

2. Create two route tables: one for each private subnet.

3. Edit the route table for the first private subnet.

4. Add a default route (0.0.0.0/0) pointing to the NAT Gateway in the same Availability Zone.

5. Associate this route table with the first private subnet.

6. Repeat the process for the second private subnet, associating it with the corresponding route table.

𝐒𝐭𝐞𝐩 𝟓: 𝐋𝐚𝐮𝐧𝐜𝐡 𝐄𝐂𝟐 𝐈𝐧𝐬𝐭𝐚𝐧𝐜𝐞𝐬 𝐢𝐧 𝐚𝐧 𝐀𝐮𝐭𝐨 𝐒𝐜𝐚𝐥𝐢𝐧𝐠 𝐆𝐫𝐨𝐮𝐩:

1. In the EC2 Dashboard, go to “Launch Configurations.”

2. Create a launch configuration specifying the instance type, security group, IAM role, and other details.

3. Choose the Amazon Machine Image (AMI) that you want to use for your instances.

4. Define the number of instances and choose the subnets in different Availability Zones.

5. Configure the Auto Scaling group to use the launch configuration and specify scaling policies based on your needs.

𝐒𝐭𝐞𝐩 𝟔: 𝐒𝐞𝐭 𝐔𝐩 𝐚𝐧 𝐀𝐩𝐩𝐥𝐢𝐜𝐚𝐭𝐢𝐨𝐧 𝐋𝐨𝐚𝐝 𝐁𝐚𝐥𝐚𝐧𝐜𝐞𝐫 (𝐀𝐋𝐁):

1. In the EC2 Dashboard, go to “Load Balancers.”

2. Click “Create Load Balancer.”

3. Choose “Application Load Balancer.”

4. Configure the ALB with listeners, target groups, and associated instances in the private subnets.

5. Create the ALB.

𝐒𝐭𝐞𝐩 𝟕: 𝐓𝐞𝐬𝐭 𝐚𝐧𝐝 𝐕𝐚𝐥𝐢𝐝𝐚𝐭𝐞 𝐭𝐡𝐞 𝐒𝐞𝐭𝐮𝐩:

1. Verify that instances are created in both Availability Zones and that the Auto Scaling group can automatically adjust instance counts based on demand.

2. Ensure that the ALB distributes incoming requests to your instances.

3. Test network connectivity between instances in different subnets to validate the networking setup.

4. Validate that the NAT gateways are working properly, and instances in the private subnets can access the internet.
