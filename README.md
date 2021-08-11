# aws_demo
# Pre-req:
  1. Tower Instance,
  2. AWS (IAM) Role configured as a variable in the ansible ./role/<role_name>variables/main.yml, 
  and defined and configured in Tower - I used iam_ansible_role referenced in ./role/<role_name>variables/main.yml.
  3. Install the following requirements:
      - ansible-galaxy collection install amazon.aws (to allow you to use the aws modules)
      - sudo yum install python3
      - sudo python get-pip.py
      - sudo pip install boto
      - sudo pip install boto3
      - sudo pip install botocore

  4. Dynamic Inventory in Tower - I used this as a guide: https://faun.pub/lets-do-devops-dynamic-host-inventories-in-aws-on-ansible-awx-tower-55347a279ad2
  5. A role/user/group in AWS IAM with the permissions to create and manage VPC, SG, EC2, AWS Keys 

# Guides I referenced to configure my Tower 
  https://faun.pub/lets-do-devops-dynamic-host-inventories-in-aws-on-ansible-awx-tower-55347a279ad2

# Plays I referenced to build my roles
  http://blog.rolpdog.com/2015/09/manage-stock-windows-amis-with-ansible.html
  http://blog.rolpdog.com/2015/09/manage-stock-windows-amis-with-ansible_3.html
  https://blog.kloud.com.au/2019/03/13/using-ansible-to-deploy-an-aws-environment/
  https://faun.pub/create-an-aws-vpc-subnet-security-group-and-acl-using-ansible-5a16aaa1042e
  useful intra role / dynamic variable communication (issue lloyd assisted with):
  https://spohnz.com/getting-aws-provisioned-with-everything-you-need-to-host-a-website-using-ansible-29-ckek4293900bctbs16bpy1evo

# Note.
  1. The playbooks are written in such a way that each role should be able to run independendantly, and only requires the correct tagging be done
  in your cloud environment - for example - when defining a subnet, a vpc_id is required as an input, my playbook, would go search/filter for a vpc with a 
  specific tag named (for example tag: test) and find the vpc_id, and then attach the subnet, to the vpc tagged test (any tag can be used).
  
  2. Remember that in AWS the order of dependencies are (for AWS in general):
     - EC2 instance depends on the SG and VPC as it requires a Security Group ID and a VPC Subnet ID
     - SG is dependant on the VPC as it requires a VPC ID
     - VPC Subnet is dependant on the VPC as it requires a VPC ID
     - VPC (not dependant on anything)
     - should you not have a vpc, subnet or security group - your ec2 play will default to a default vpc, subnet and sg - so you technically don't need them, I just 
       included these as best practice.
  3. These roles can be used independantly and references tags in aws key:value (i.e environment:test) attached to objects like the vpc, subnet, sg and ec2.




