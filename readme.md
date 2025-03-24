		-----------------------------------------------------------------------------
			Assignment 3: Configuration Management Automation with Ansible
		-----------------------------------------------------------------------------
	

PREQUISTES:

1. Amazon EC2 should be deployed.
	- We need 4 instances in two different availability zones.
	- 4 instances consists of two RPM based and two Debian based instances.
2. Install ansible 
	- sudo yum install -y ansible
3. Install PythonBoto3
	- sudo yum install -y python-boto3


STEPS:

1. Change Directory to A3-Completed/ansible

2. Install ansible if not installed already.

3. Update the hosts.txt file in the directory
	- ip address of predeployed instances should be updated.

4. Update /etc/ansible/ansible.cfg file.
	- inventory should be mentioned as hosts.txt file we created.

5. Use ad hoc command to ping the predeployed instances.
	- ansible -i hosts.txt linux -m ping

6. Instance should be predeployed. - 2xDebian & 2xRedHat
	- ansible -i hosts.txt linux -m setup -a "filter=ansible_os_family"

7. Update /etc/ansible/ansible.cfg file to use dynamic inventory.
	- under [inventory], update " enable_plugins = aws_ec2 "
	- ansible-inventory -i aws_ec2.yaml --graph

8. Install python-boto3 if not instaled already.
	
9. Run playbook-role.yaml
			- ansible-playbook -i aws_ec2.yaml playbook-role.yaml	
			- This should install static website on all four predeployed ec2 instances.

10. Create a new Amazon EC2 insance using EC2 Management Console
	- Add tag: Distro = "Amazon"

11. Run playbook-role.yaml again.
	- ansible-playbook -i aws_ec2.yaml playbook-role.yaml

12. Using ad hoc command verify that static website is installed all instances.
	- ansible -i aws_ec2.yaml tag_Ubuntu -m uri -a "url=http://localhost" -u ubuntu --private-key ~/.ssh/linux
	- ansible -i aws_ec2.yaml tag_Amazon -m uri -a "url=http://localhost" -u ec2-user --private-key ~/.ssh/linux
