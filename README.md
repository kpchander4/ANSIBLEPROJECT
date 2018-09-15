# ANSIBLEPROJECT
This ansible script will perform the following tasks

	1. For all
		- set intance hostname
		- pouplate /etc/hosts file with all hosts in inventory file
		- secure ssh server

	2. For database server
		- install mysql server
		- configure mysql server
		- set root password to 'password'
		- delete annoynomous mysql users
		- remove default test database
		- create opencms database
		- create opencms user with privileges to opencms database

	3. For app server
		- install jdk
		- install tomcat7
		- setup environment variables
		- install opencms
		- configure opencms
		- auto setup opencms

	4. For web server
		- install apache2
		- enable required modules
		- enable virtualhosts that connects to opencms

Prerequisites:
	1. AWS
		- setup AWS environment with terraform in part 1

	2. Local testing machine
		- update 'ansibile/inventory' file with with actual instance ip addresses
		- update local machine host file to point web01.test.com to WEB01's public elastic ip address

	3. MGMT01 instance (to access instance, ssh to it's public EIP as ubuntu user with AWS private key)
		- copy ssh private key used for AWS instances to /home/ubuntu/.ssh/
		- chmod permission of ssh private key in /home/ubuntu/.ssh/ to 600
		- copy 'config' file to /home/ubuntu/.ssh/
		- update config file in /home/ubuntu/.ssh/config and update the AWS-PRIVATE-KEY-FILENAME
		- copy 'ansible' folder to /home/ubuntu/ansible (make sure you update the inventory file before you copy)
		- copy 'install_ansible.sh' to /home/ubuntu
		- run install_ansible.sh to install ansible e.g. 'sh install_ansible.sh'

How to run the code:
	1. cd to /home/ubuntu/ansible
	2. run 'ansible-playbook -i inventory provision.yml -u ubuntu -l all'
	3. for 1st run, the opencms autoinstall will fail
	4. repeat step 2 again

How to test the site:
	1. On local test machine, visit 'http://web01.test.com/opencms/system/login'
