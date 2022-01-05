## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the __YAML___ file may be used to install only certain pieces of it, such as Filebeat.

  - install-elk.yml

This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly protected and redundant_____, in addition to restricting _unauthorized traffic/overwhelming network requests (DDos)____ to the network.
-What aspect of security do load balancers protect? What is the advantage of a jump box?_
Load balancers aid in the protection of primary webservers from traffic overload. This is done by offloading high volume traffic from the primary server to a secondary pool of servers meant to relieve the network load and distribute the load across the servers. A Jumpbox ensures that the only external access point to the network is the Jumpbox. There is no way to navigate through our network without first landing on the Jumpbox and providing rules that allow traversing through the network. 

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the __configuration files___ and system __files___.
-What does Filebeat watch for?_Filebeat monitors log files and events specified by the user. These logs and events are compiled for review through tools such as elasticsearch or Logstash for indexing

-What does Metricbeat record?_Metricbeat takes collected data and sends it to a specified output. Known as a metric shipper, metricbeat can automatically insert collected metrics directly into elasticsearch or Logstash. Metricbeat can collect metrics from many services such as Apache, MySQL, and Redis.

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box |Gateway   | 10.0.0.4   | Linux            |
| Web1     |DVWA1     | 10.0.0.5   | Linux            |
| Web2     |DVWA2     | 10.0.0.6   | Linux            |
| ELK      |ELK/Kibana| 10.2.0.4   | Linux            |
 
### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the __Jumpbox Provisioner___ machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- 67.176.49.44
Machines within the network can only be accessed by _the Jumpbox____.
-Which machine did you allow to access your ELK VM? What was its IP address?_My personal host machine (IP: 67.176.49.44)

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes                 | 67.176.49.44         |
| Web1     | No                  | 10.0.0.4 & 10.0.0.5  |
| Web2     | No                  | 10.0.0.4 & 10.0.0.6  |
| ELK      | Yes (HTTP)          | 10.2.0.4             |
### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
-What is the main advantage of automating configuration with Ansible?_Playbooks allow for automated configuration of services across all machines within a network using that container. This means that all DVWA’s within the network can be configured at the same time instead of individually. 

The playbook implements the following tasks:
-In 3-5 bullets, explain the steps of the ELK installation play. E.g., install Docker; download image; etc._
- Install docker.io
- Install python3-pip
- Install Docker module
- Download and launch docker elk container
- Enable service docker on boot

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance. gifted_lamport is the container being used.



### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- Web1 (10.0.0.5), Web2 (10.0.0.6)

We have installed the following Beats on these machines:
- Filebeat and Metricbeat

These Beats allow us to collect the following information from each machine:
- In 1-2 sentences, explain what kind of data each beat collects, and provide 1 example of what you expect to see. E.g., `Winlogbeat` collects Windows logs, which we use to track user logon events, etc._
Filebeat monitors log files and log events. Metricbeat looks out for any information in the file system which has been manipulated and automatically sends it to Elasticsearch or similar tool for indexing and review.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the __ansible configuration___ file to __run the playbook___.
- Update the __ansible host___ file to include IP addresses of machines that beats will be deployed on.
- Run the playbook, and navigate to _Web1 and Web2__ to check that the installation worked as expected.

_TODO: Answer the following questions to fill in the blanks:_
- _Which file is the playbook? Where do you copy it?_
- _Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?_
- _Which URL do you navigate to in order to check that the ELK server is running?

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc. 
ansible-playbook install-elk.yml
