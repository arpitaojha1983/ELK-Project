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
 - filebeat configuration.yml​
 - ansible-config.yml
 - hosts.yml
 - install-elk.yml
 - metricbeat-configuration.yml
 - metricbeat-playbook.yml


This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
- Beats in Use and Machines Being Monitored
- How to Use the Ansible Build
​
​
### Description of the Topology
​
The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.
​
Load balancing ensures that the application will be highly available, in addition to restricting permissions to the network.

The load balancer aids in security by offloading traffic from a corporate server to a public cloud provider. Integrating an ELK (Elasticsearch, Logstash, and Kibana) server allows users to easily monitor the vulnerable VMs for changes to the file names and watch system metrics.
Keeping the networks protected from the open web and balancing the incoming traffic preventing DDOS attacks, thereby providing a more efficient application. 

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the log files and system performance with the use of Filebeat and Metricbeat.
​
Filebeat monitors the logs in the specified locations. It detects changes to the filesystem. It collects logs and forwards them to Elastisearch or Logstash for indexing

Metricbeat detects changes in system metrics such as CPU usage. 
​
The configuration details of each machine may be found below.
​
| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 10.0.0.1   |  Linux  Ubuntu   |
| DVWA-VM1 |   WebApp | 10.0.0.5   |  Linux  Ubuntu   |
| DVWA-VM1 |   WebApp | 10.0.0.6   |  Linux  Ubuntu   |
| DVWA-VM3 |   WebApp | 10.0.0.7   |  Linux  Ubuntu   |
| ELK VM   |    ELK   | 10.0.0.4   |  Linux  Ubuntu   |


​
### Access Policies
​
The machines on the internal network are not exposed to the public Internet.
​
Only the Jumpbox Provisioner machine can accept connections from the Internet. Access to this machine is only allowed from the designated public IP address.
Here my local machine IP which is 174.52.113.43

This address changes each time the machine is powered down and restarted.

Machines within the network can only be accessed by peer servers. The Jumpbox Provisioner connects via SSH to the Webservers (Web 1, Web 2 & Web 3) and the ELK Server. The Web Server machines send logs to the ELK Server to be forwarded for indexing.

A summary of the access policies in place can be found in the table below.
​
| Name     | Publicly Accessible | Allowed IP Addresses      |
|----------|---------------------|---------------------------|
| Jump Box |    Yes              | 10.0.0.0 to 10.255.255.255
|   ELk Vm |    NO               | 10.1.0.0 to 10.255.255.255
|   VM1    |    NO               | 10.1.0.0 to 10.255.255.255
|   VM2    |    NO               | 10.1.0.0 to 10.255.255.255
|   VM3    |    No               | 10.1.0.0 to 10.255.255.255



### Elk Configuration
​
Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because of the simple syntax used in creating the playbooks in YAML allowed to quickly install, update, and add the web servers to the network using the same playbooks.

The playbook implements the following tasks:

-Download and launch docker web container
-Ansible is installed on the Jump Box VM to distribute containers to other VMs on the network
-Ansible playbooks are used to install the ELK stack container on the ELK server and a 'Beats' containers on the Web servers
-Install docker on all network machines so they will be able to recieve and install containers

The following screenshot displays the result of running docker ps after successfully configuring the ELK instance.
https://drive.google.com/file/d/1jD1tGovUjLb3iG5Sn3d01pkXQox3vEOq/view?usp=sharing


### Beats in Use and Machines Being Monitored
This ELK server is configured to monitor the following machines:

DVMA-VM1
DVMA-VM2
DVWA-VM3

We have installed the following Beats on these machines:

Filebeat --> Filebeat collects and forwards log data from the machines it is installed on and sends this information to the ELK stack server for processing. This information can then be viewed through Kibana through customizable charts and tables.

Metricbeat --> Metricbeat detects changes in system metrics like monitoring performance like CPU , memory and load.






### How to Use the Ansible Build

Downloading the playbook and updating files

It automates tasks that are either cumbersome or repetitive or complex like configuration management, cloud provisioning, software deployment, and intra-service orchestration. 

Ansible is used for the multi-tier deployments and it models all of IT infrastructure into one deployment instead of handling each one separately. There are no agents and no custom security architecture is required to be used in the Ansible architecture. The deployment is simple plain English like language that is used in Ansible called YAML 
​
The playbook implements the following tasks:
1. ssh sysadmin@40.87.110.143  --> ssh into JumpboxProvisioner from local desktop
2. sudo container list -a  → View list of containers in jumpbox
3. sudo docker start 54d35156296e  → start the container
4. sudo docker attach 54d35156296e  → attaching the docker
5. root@54d35156296e:/etc/ansible# ssh sysadmin@13.66.186.63  → login into ELk VM from jumpbox ansible container
6.  sysadmin@ELK-VM1:~$ sudo docker ps  -->Check the container running 
7. nano /etc/ansible/hosts
add additional private IPs under [webservers]--> Add DVWAs to hosts file:
8. ansible-playbook /etc/ansible/install-elk.yml -->Run playbook to update elk:
9. copy filebeatconfig.yml file to /etc/ansible/files/
10. ansible-playbook /etc/ansible/roles/filebeatplaybook.yml--> Run playbook for filebeat
11. Open a new browser on Personal Workstation, navigate to (ELK-Server-PublicIP:5601/app/kibana) - This will bring up Kibana Web Portal

http://[40.87.110.143]:5601/app/kibana.
