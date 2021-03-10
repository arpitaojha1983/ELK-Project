## Automated ELK Stack Deployment
​
The files in this repository were used to configure the network depicted below.
​
https://drive.google.com/file/d/1E0lsCUnmgaqCoaOOzwq1GA3nNnesh8iB/view?usp=sharing
​
These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the YML file may be used to install only certain pieces of it, such as Filebeat.
​
 - install-elk.yml
 - filebeat-playbook.yml
 - filebeat config.yml​


This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
 - Beats in Use
 - Machines Being Monitored
- How to Use the Ansible Build
​
​
### Description of the Topology
​
The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.
​
Load balancing ensures that the application will be highly available, in addition to restricting permissions to the network.
- _TODO: What aspect of security do load balancers protect? 








What is the advantage of a jump box?_ 
​
Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the _____ and system _____.
- _TODO: What does Filebeat watch for?_
- _TODO: What does Metricbeat record?_
​
The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.
​
| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 10.0.0.1   | Linux            |
| TODO     |          |            |                  |
| TODO     |          |            |                  |
| TODO     |          |            |                  |
​
### Access Policies
​
The machines on the internal network are not exposed to the public Internet.
​
Only the _jumpbox____ machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- _TODO: 174.52.113.43 ( my local machine Ip)


​
Machines within the network can only be accessed by _jumpbox by ssh and http through network security group____.
- _TODO: Which machine did you allow to access your ELK VM? What was its IP address?_ Jumpbox  and Ip is 40.87.110.143
​
A summary of the access policies in place can be found in the table below.
​
| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box |    Yes              | 10.0.0.0 to 10.255.255.255
|   ELk Vm |    yes              | 10.1.0.0 to 
|   VM1    |    NO               |
​|   VM2    |    NO               |
|   VM3    |    No               |




































### Elk Configuration
​
Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because…




It automates tasks that are either cumbersome or repetitive or complex like configuration management, cloud provisioning, software deployment, and intra-service orchestration. 
Ansible is used for the multi-tier deployments and it models all of IT infrastructure into one deployment instead of handling each one separately. There are no agents and no custom security architecture is required to be used in the Ansible architecture. The deployment is simple plain English like language that is used in Ansible called YAML 
​
The playbook implements the following tasks:
1. ssh sysadmin@40.87.110.143  --> ssh into jumpbox
2. sudo container list -a  → list of containers in jumpbox
3. sudo docker start 54d35156296e  → start the container
4. sudo docker attach 54d35156296e  → attaching the docker
5. root@54d35156296e:/etc/ansible# ssh sysadmin@13.66.186.63  → login into ELk VM from jumpbox ansible container
6.  sysadmin@ELK-VM1:~$ sudo docker ps  -->Check the container running 


​
The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.


​https://drive.google.com/file/d/1jD1tGovUjLb3iG5Sn3d01pkXQox3vEOq/view?usp=sharing


  

​






























### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- 10.0.0.5
- 10.0.0.6
- 10.0.0.7


​
We have installed the following Beats on these machines:
- Filebeat
-  MetricBeat
​
These Beats allow us to collect the following information from each machine:
- FileBeat allow us to keep track of who is logging in to these servers and monitors the behaviors.
- Also Metricbeats for  monitoring performance like CPU , memory and load.




### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned:
​
SSH into the control node and follow the steps below:
- Copy the filebeat-config.yml file to /etc/ansible/files.
- Update the config file to include private ip of Elk server
- Run the playbook, and navigate to ELK-Server-PublicIP:5601/app/kibana to check that the installation worked as expected.
​
_TODO: Answer the following questions to fill in the blanks:_
- _Which file is the playbook? Where do you copy it?_

install-elk.yml - used to install ELK Server
filebeat-playbook.yml - Used to install and configure Filebeat on Elk Server and DVWA servers

I copied into /etc/ansible/



- _Which file do you update to make Ansible run the playbook on a specific machine? 
/etc/ansible/hosts




How do I specify which machine to install the ELK server on versus which to install Filebeat on?_


We will install the ELK server on that machine from where we want to monitor the logs , which we will refer to as our ELK Server. 
Filebeat will be installed on all of the client servers that we want to gather logs for, which we will refer to collectively as our Client Servers.



- _Which URL do you navigate to in order to check that the ELK server is running?
http://[40.87.110.143]:5601/app/kibana. ( ELK VM public ip)
​




_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._


* ssh sysadmin@jumpbox-privateIP
* sudo docker container list -a - Locate the ansible container
* sudo docker start
* sudo attach docker
* cd /etc/ansible
* nano hosts (update IP on[webservers][elkservers]
* nano ansible.cfg (remote_user to which server you want to use)
* ansible-playbook install-elk.yml 
* Open a new browser on Personal Workstation, navigate to (ELK-Server-PublicIP:5601/app/kibana) - This will bring up Kibana Web Portal




