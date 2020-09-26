# Homework13
HW13
---
- name: Install metric beat
  hosts: webservers
  become: true
  tasks:
    # Use command module
  - name: Download metricbeat
    command: curl -L -O https://artifacts.elastic.co/downloads/beats/metricbeat/metricbeat-7.4.0-amd64.deb

    # Use command module
  - name: install metricbeat
    command: dpkg -i metricbeat-7.4.0-amd64.deb

    # Use copy module
  - name: drop in metricbeat config
    copy:
      src: /etc/ansible/files/metricbeat-config.yml
      dest: /etc/metricbeat/metricbeat.yml

    # Use command module
  - name: enable and configure docker module for metric beat
    command: metricbeat modules enable docker

    # Use command module
  - name: setup metric beat
    command: metricbeat setup

    # Use command module
  - name: start metric beat
    command: service metricbeat start
 BIN +109 KB Images/Kibana_Home_Page.png 
Binary file not shown.
 BIN +62.1 KB Images/Metricbeat_Charts.png 
Binary file not shown.
 BIN +18.2 KB Images/Module_Status.png 
Binary file not shown.
 BIN +117 KB Images/XCorp_Red_Team_Network_Diagram.png 
Binary file not shown.
 BIN +8.9 KB Images/sudo_docker_ps.png 
Binary file not shown.
 134  README.md 
@@ -1 +1,133 @@
# Automated_ELK_Stack_Deployment
# Automated_ELK_Stack_Deployment

The files in this repository were used to configure the network depicted below.

![XCorp_Red_Team_Network_Diagram](Images/XCorp_Red_Team_Network_Diagram.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the install-elk, filebeat-playbook.yml, metricbeat-playbook.yml file may be used to install only certain pieces of it, such as Filebeat.

[install-elk.yml](Ansible_YML_Scripts/install-elk.yml)
[filebeat-configuration.yml](Ansible_YML_Scripts/filebeat-configuration.yml)
[filebeat-playbook.yml](Ansible_YML_Scripts/filebeat-playbook.yml)
[metricbeat-configuration.yml](Ansible_YML_Scripts/metricbeat-configuration.yml)
[metricbeat-playbook.yml](Ansible_YML_Scriptsmetricbeat-playbook.yml)

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
- Beats in Use
- Machines Being Monitored
- How to Use the Ansible Build


## Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the Damn Vulnerable Web Application.

Load balancing ensures that the application will be highly resilient, in addition to restricting access to the network.

The load balancer helps to ensure there is access to network resources is redundant.

Having access to the network limited to a single machine and a single IP.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the system files and system logs.

Filebeat collects event log data and authenticates their integrity.

Metricbeat collects metrics on the system and services running on a server.

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name     | Function | IP Address | Operating System |
|-------------|-------------|----------------|--------------------------|
| Jump Box | Gateway  | 10.0.0.4   | Linux       |
| Web-1      |Web Server| 10.0.0.10  | Linux       |
| Web-2      |Web Server| 10.0.0.11  | Linux       |
| Web-3      |Web Server| 10.0.0.5    | Linux       |
|ELK | Web Server | 10.1.0.4 | Linux |

## Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump Box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP address:
- 71.197.72.213

Machines within the network can only be accessed by the Jump Box.

The ELK VM can only be accessed through the Ansible Container inside the Jump Box 10.0.0.4

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
|SSHJumpBox |        Yes         |     10.0.0.4    |
|   Allow-RDP   |          Yes        | 71.197.72.213 |


## Elk Configuration

Ansible was used to automate the configuration of the ELK machine. No configuration was performed manually, which is advantageous because...

Using Ansible allows the quick deployment of applications without the need of writing custom code for each machine by instead writing a playbook that can be applied to all the machines.

The playbook implements the following tasks:
-  Docker.io
- Install pip3
- Install Docker python module
- Increase virtual memory
- use mem
- downloaded and launched a docker elk container

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![sudo docker ps](Images/sudo_docker_ps.png)

## Target Machines & Beats
This ELK server is configured to monitor the following machines:
Web-1 10.0.0.10
Web-2 10.0.0.11
Web-3 10.0.0.5

We have installed the following Beats on these machines:
Filebeat
Metricbeat

These Beats allow us to collect the following information from each machine:

Filebeat collects event log data that can then be analyzed using Kibana and authenticates their integrity.
Metricbeat collects metrics on the system and services running on a server and can be analyzed using Kibana.

## Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the install-elk.yml file to /etc/ansible/files/
- Update the hosts file to include the IP addresses of the machines you want to run the playbooks on.
- Run the playbook, and navigate to Kibana to check that the installation worked as expected.




The DATA from this sent to the ELK can be analyzed by going to:
http://52.183.8.231:5601/app/kibana
![Kibana_Home_Page](Image/Kibana_Home_Page.png)

## Commands for downloading the playbooks
install-elk.yml
`curl https://github.com/BenjaminBartholomew/Automated_ELK_Stack/blob/master/Ansible_YML_Scripts/install-elk.yml  > /etc/ansible/files/install-elk.yml’
filebeat-configuration.yml
`curl https://github.com/BenjaminBartholomew/Automated_ELK_Stack/blob/master/Ansible_YML_Scripts/filebeat-configuration.yml > /etc/ansible/files/filebeat-configration.yml’

filebeat-playbook.yml
`curl https://github.com/BenjaminBartholomew/Automated_ELK_Stack/blob/master/Ansible_YML_Scripts/filebeat-playbook.yml > /etc/ansible/files/filebeat-playbook.yml’
metricbeat-configuration.yml
`curl https://github.com/BenjaminBartholomew/Automated_ELK_Stack/blob/master/Ansible_YML_Scripts/metricbeat-configuration.yml > /etc/ansible/files/filebeat-configuration.yml’

metricbeat-playbook.yml
`curl https://github.com/BenjaminBartholomew/Automated_ELK_Stack/blob/master/Ansible_YML_Scripts/metricbeat-playbook.yml > /etc/ansible/files/filebeat-configuration.yml’
