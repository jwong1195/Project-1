# Project-1
## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.
https://docs.google.com/document/d/1udNiXle-8Jg8JjqALuV09bbW76fAyTPRJNmvDWbG_iE/edit 

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the yml file may be used to install only certain pieces of it, such as Filebeat.
Install-elk.yml: https://docs.google.com/document/d/1qs_nNRuJb8H-th9l5-lb8XpwVwSQERAHHywuSKeNc-M/edit 

Filebeat-playbook.yml: https://docs.google.com/document/d/1CmM19TBACrrj6FcebCmDeVHpcYdNCbyhcANpzBugO7U/edit 

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
- Beats in Use
- Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting access to the network.

Load balancers protect the system from DDoS attacks, because it distributes the traffic across the machines instead of just one machine.

The advantage of a jump box is that it makes it easier to monitor who has access and it can be more secure as it gives a user access from a single machine.


Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the jumpbox and system network.

Filebeat collects data about the file system, so that analysts can monitor files for suspicious changes.
Metricbeat collects specific information or metrics about the machines in the network, such as the uptime and CPU usage.

The configuration details of each machine may be found below.
-----------------------------------------------------------------------------
| Name                 | Function          |  IP Address | Operating System |
| ---------------------|-------------------| ------------|------------------|
| Jump-Box-Provisioner | Gateway           | 10.0.0.1    | Linux            |
| Web-1                | Web Server        | 10.0.0.5    | Linux            |
| Web-2                | Web Server        | 10.0.0.6    | Linux            |
| Elk-Stack-VM         | Log Management    | 10.1.0.4    | Linux            |
-----------------------------------------------------------------------------


### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jumpbox machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
My local machine’s public IP address

Machines within the network can only be accessed by Jumpbox Provisioner.

The Jumpbox Provisioner Machine has access to the Elk-Stack-VM. Its IP address was 40.121.138.196 / 10.0.0.4

A summary of the access policies in place can be found in the table below.
-----------------------------------------------------------------------------------------------------------------------
| Name                 | Publicly Accessible |                     Allowed IP Addresses                               |
| ---------------------|---------------------| -----------------------------------------------------------------------|
| Jump-Box-Provisioner | No                  | My local machine’s IP address                                          |
| Web-1 and Web-2      | No                  | My local machine’s IP address from port 5601                           |                           
| Elk-Stack-VM         | No                  | Through the load balancer (20.85.217.178), which is connected to the   |
|                      |                     | Jump-Box-Provisioner (40.121.138.196)                                  |
-----------------------------------------------------------------------------------------------------------------------


### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because it streamlines the process of installing and updating services across multiple machines. 

The main advantage of automating configuration with Ansible is that it streamlines the process of installing services and updating them across multiple machines.

The playbook implements the following tasks:
-  Installs docker.io, python3-pip, and Docker module
-  Sets vm.max_map_count to 262144
-  Downloads and launches a docker container on the following published ports:
          - 5601:5601
          - 9200:9200
          - 5044:5044
-  Enables docker service

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.
https://docs.google.com/document/d/1Cy7L0rmPbR2siBoiymdj9MEB7KAEGFdyo1_P5zaGFEE/edit 

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
Web-1 (10.0.0.5) and Web-2 (10.0.0.6), which are both connected to the Jump-box-Provisioner machine

We have installed the following Beats on these machines:
- Filebeats

These Beats allow us to collect the following information from each machine:
“Filebeat monitors the log files or locations that you specify, collects log events, and forwards them either to Elasticsearch or Logstash for indexing.” This includes server logs.

Work Cited: 
Elasticsearch B.V. (n.d.). Filebeat overview. Elastic. https://www.elastic.co/guide/en/beats/filebeat/current/filebeat-overview.html#:~:text=Filebeat%20is%20a%20lightweight%20shipper,Elasticsearch%20or%20Logstash%20for%20indexing.


### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the configuration file to your Ansible container
- Update the hosts file to include your Elk server
- Run the playbook, and navigate to Kibana to check that the installation worked as expected.

Which file is the playbook? 
The Filebeat-playbook.yml: https://docs.google.com/document/d/1CmM19TBACrrj6FcebCmDeVHpcYdNCbyhcANpzBugO7U/edit 

Where do you copy it?
I copied the Filebeat-playbook.yml file to the /etc/ansible/roles/ directory

Which file do you update to make Ansible run the playbook on a specific machine? 
I updated the hosts file to make Ansible run the playbook on a specific machine.
https://docs.google.com/document/d/1UIIo9CO60ZmN_OD6ROtbDz_h0J_ZS81nr2wEcCx-QVY/edit  

How do I specify which machine to install the ELK server on versus which to install Filebeat on?
I adjust the host on the playbook file to specify which machine to install the ELK server on versus which to install Filebeat on.

Which URL do you navigate to in order to check that the ELK server is running?
http://168.61.20.54:5601/app/kibana#/home 
