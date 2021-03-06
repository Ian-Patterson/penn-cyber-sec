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

[Screen Shot zealous_lalande](https://user-images.githubusercontent.com/89041734/143973833-095f5997-4a9e-49b4-bf95-c9130c986762.png)

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
- Which file is the playbook?  
  - Ansible: My First Playbook
  - Filebeat: Filebeat Playbook
  - Metricbeat: Metricbeat Playbook
- Where do you copy it?
  - etc/ansible/
- _Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on? 
  - etc/ansible/hosts 
- _Which URL do you navigate to in order to check that the ELK server is running? 
  - http://20.120.78.93/app/kibana

| Command                                 | Function                                             |
|-----------------------------------------|------------------------------------------------------|
| sudo apt-get update                     | update all packages                                  |
| sudo apt install docker.io              | install docker application                           |
| sudo docker pull cyberxsecurity/ansible | pull docker container file                           |
| ssh-keygen                              | create ssh key for VM's                              |
| sudo cat .ssh/id_rsa.pub                | view public ssh key                                  |
| ssh azadmin@20.115.64.3                 | log into Jumpbox                                     |
| sudo docker container list -a           | list all docker containers                           |
| sudo docker start zealous_lalande       | start docker container zealous_lalande               |
| sudo docker attach zealous_lalande      | ssh into zealous_lalande container                   |
| sudo docker ps -a                       | lists all active/inactive containers                 |
| nano /etc/ansible hosts                 | edit hosts file                                      |
| nano /etc/ansible/ansible.cfg           | edit ansible configuration file                      |
| nano /etc/ansible/pentest.yml           | edit the My Playbook file                            |
| ssh azadmin@10.0.0.7                    | ssh into Web-1 VM                                    |
| ssh azadmin@10.0.0.6                    | ssh into Web-2 VM                                    |
| ssh azadmin@10.4.0.4                    | ssh into Elk VM                                      |
| nano filebeat-config.yml                | create and edit filebeat configuration file          |
| nano filebeat-playbook.yml              | create YAML file to install filebeat on webservers   |
| nano metricbeat-config.yml              | create metricbeat configuration file and edit        |
| nano metricbeat-playbook.yml            | create YAML file to install metricbeat on webservers |
|                                         |                                                      |
|                                         |                                                      |
