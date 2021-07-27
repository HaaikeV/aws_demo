# aws_demo
Pre-req:
  Tower Instance
  AWS (IAM) Role configured and variable in ansible role defined and configured in Tower.

Plays I used to build my roles
http://blog.rolpdog.com/2015/09/manage-stock-windows-amis-with-ansible.html
http://blog.rolpdog.com/2015/09/manage-stock-windows-amis-with-ansible_3.html
https://blog.kloud.com.au/2019/03/13/using-ansible-to-deploy-an-aws-environment/
https://faun.pub/create-an-aws-vpc-subnet-security-group-and-acl-using-ansible-5a16aaa1042e
useful intra role / dynamic variable communication (issue lloyd assisted with):
https://spohnz.com/getting-aws-provisioned-with-everything-you-need-to-host-a-website-using-ansible-29-ckek4293900bctbs16bpy1evo

Note.
The playbooks are written in such a way that each role should be able to run independendantly, and only requires the correct tagging be done
in your cloud environment - for example - when defining a subnet, a vpc_id is required as an input, my playbook, would go search/filter for a vpc with a 
specific tag named (for example tag: test) and find the vpc_id, and then attach the subnet, to the vpc tagged test (any tag can be used).



