# penn-cyber-sec
## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

https://github.com/Ian-Patterson/penn-cyber-sec/blob/a2c12a93265c59bbaecb31fa5fada815265e3521/Diagrams/Red%20Team%20diagram.drawio.png

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the _____ file may be used to install only certain pieces of it, such as Filebeat.

  - https://github.com/Ian-Patterson/penn-cyber-sec/blob/main/Ansible/config_web_vm_docker.yml
  - https://github.com/Ian-Patterson/penn-cyber-sec/blob/main/Ansible/filebeat-config.yml
  - https://github.com/Ian-Patterson/penn-cyber-sec/blob/main/Ansible/filebeat_playbook.yml
  - https://github.com/Ian-Patterson/penn-cyber-sec/blob/main/Ansible/install-elk.yml
  - https://github.com/Ian-Patterson/penn-cyber-sec/blob/main/Ansible/metricbeat-config.yml
  - https://github.com/Ian-Patterson/penn-cyber-sec/blob/main/Ansible/metricbeat-playbook.yml
  - https://github.com/Ian-Patterson/penn-cyber-sec/blob/main/Ansible/myplaybook.yml

This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting traffic to the network.
- Load balancers create resilliance by rerouting traffic from one server to another in case of DDOS attack or other availability issues

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the network and system logs.
- Filebeat monitors logfiles, collects log events and sends them to ELasticsearch or Logstash
- Metricbeat takes metics and stats and sends them Elasticsearch, Logstash, etc.

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 10.0.0.5   | Linux            |
| Web-1    | Ubuntu Server | 10.0.0.7 | Linux         |
| Web-2    | Ubuntu Server | 10.0.0.6 | Linux         |
| Elk-VM    | Ubuntu Server | 10.4.0.4 | Linux         |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jumpbox machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- My Public IP address through TCP 5601

Machines within the network can only be accessed by My workstation and Jumpbox Provisioner through SSH.
- Which machine did you allow to access your ELK VM? What was its IP address?_
  Jumpbox Provisioner IP: 10.0.0.6

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes                 | My local machine Public IP   |
| Web-1    | No                    |  SSH:22 10.0.0.5           |
| Web-2    | No                    |  SSH:22 10.0.0.5           |
| Elk-VM   | No                    | SSH:22 10.0.0.5 & TCP:5601 My local public IP|

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because it allows for the creation of hosts and then executable playbooks which contain scripts to be completed on the remote machine 

The playbook implements the following tasks:
- Installs docker.io
- installs Python3-pip and then installs docker module
- Downloads and Elk Docker Container Image

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![TODO: Update the path with the name of your screenshot of docker ps output][Screen Shot zealous_lalande](https://user-images.githubusercontent.com/89041734/143973833-095f5997-4a9e-49b4-bf95-c9130c986762.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- Web-1: 10.0.0.7
- Web-2: 10.0.0.6

We have installed the following Beats on these machines:
-Filebeat
-Metricbeat

These Beats allow us to collect the following information from each machine:
- Filebeat collects specific log files from the system such as Apache logs
- Metricbeat is used for system monitoring: memory, CPU, file system, etc. 

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the Install Elk File file to ansible container.
- Update the /etc/ansible/hosts file to include IP address of VM
- Run the playbook, and navigate to http://YourIPaddress:5601/app/kibana to check that the installation worked as expected.

Answer the following questions to fill in the blanks:_
- _Which file is the playbook?  
- Ansible: My First Playbook
- Filebeat: Filebeat Playbook
- Metricbeat: Metricbeat Playbook
- Where do you copy it?
 - etc/ansible/
- _Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?_ 
- etc/ansible/hosts 
- _Which URL do you navigate to in order to check that the ELK server is running? 
- http://20.120.78.93/app/kibana

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._
ssh-keygen 	create a ssh key for setup VM's
sudo cat .ssh/id_rsa.pub 	to view the ssh public key
ssh azadmin@Jump-Box-Provisioner IP address 	to log into the Jump-Box-Provisioner
sudo docker container list -a 	list all docker containers
sudo docker start dremy_elbakyan 	start docker container dremy_elbakyan
sudo docker ps -a 	list all active/inactive containers
sudo docker attach dremy_elbakyan 	effectively sshing into the dremy_elbakyan container
cd /etc/ansible 	Change directory to the Ansible directory
ls -laA 	List all file in directory (including hidden)
nano /etc/ansible/hosts 	to edit the hosts file
nano /etc/ansible/ansible.cfg 	to edit the ansible.cfg file
nano /etc/ansible/pentest.yml 	to edit the My-Playbook
ansible-playbook [location][filename] 	to run the playbook
sudo lsof /var/lib/dpkg/lock-frontend 	unlocking a locked file
ssh ansible@Web-1 IP address 	to log into the Web-1 VM
ssh ansible@Web-2 IP address 	to log into the Web-2 VM
ssh ansible@DVWA-VM3 IP address 	to log into the DVWA-VM3 VM
ssh ansible@ELKserver IP address 	to log into the ELKserver VM
exit 	to exit out of docker containers/Jump-Box-Provisioners
nano /etc/ansible/ansible.cfg 	to edit the ansible.cfg file
nano /etc/ansible/hosts 	to edit the hosts file
nano /etc/ansible/pentest.yml 	to edit the My-Playbook
ansible-playbook [location][filename] 	to run the playbook
sudo apt-get update 	this will update all packages
sudo apt install docker.io 	install docker application
sudo service docker start 	start the docker application
sudo systemctl status docker 	status of the docker application
sudo systemctl start docker 	start the docker service
sudo docker pull cyberxsecurity/ansible 	pull the docker container file
sudo docker run -ti cyberxsecurity/ansible bash 	run and create a docker container image
ansible -m ping all 	check the connection of ansible containers
curl -L -O [location of the file on the web] 	to download a file from the web
dpkg -i [filename] 	to install the file i.e. (filebeat & metricbeat)
http://20.84.136.248:5601//app/kibana 	Open web browser and navigate to Kibana Logs
nano filebeat-config.yml 	create and edit filebeat config file
nano filebeat-playbook.yml 	write YAML file to install filebeat on webservers
nano metricbeat-config.yml 	create metricbeat config file and edit it
nano metricbeat-playbook.yml 	write YAML file to install metricbeat on webservers
