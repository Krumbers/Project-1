## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![network diagram](https://user-images.githubusercontent.com/89494589/148151679-b3e128a1-e885-4c3e-be70-8bbf0a1e1b6d.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the YAML file may be used to install only certain pieces of it, such as Filebeat.

  - install-elk.yml


[Ansible Playbooks](https://github.com/Krumbers/Project-1/tree/main/Ansible)

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly protected and creates redundancy, in addition to restricting unauthorized traffic/overwhelming network requests (DDoS) to the network.
-What aspect of security do load balancers protect? What is the advantage of a jump box?
Load balancers aid in the protection of primary webservers from traffic overload. This is done by offloading high volume traffic from the primary server to a secondary pool of servers meant to relieve the network load and distribute the load across the servers. This increases avaliability of resources.
A Jumpbox ensures that the only external access point to the network is the Jumpbox. There is no way to navigate through our network without first landing on the Jumpbox and providing rules that allow traversing through the network. 

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the configuration files and system files.
-What does Filebeat watch for?
Filebeat monitors log files and events specified by the user. These logs and events are compiled for review through tools such as elasticsearch or Logstash for indexing

-What does Metricbeat record?
Metricbeat takes collected data and sends it to a specified output. Known as a metric shipper, metricbeat can automatically insert collected metrics directly into elasticsearch or Logstash. Metricbeat can collect metrics from many services such as Apache, MySQL, and Redis.

The configuration details of each machine may be found below.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box |Gateway   | 10.0.0.4   | Linux            |
| Web1     |DVWA1     | 10.0.0.5   | Linux            |
| Web2     |DVWA2     | 10.0.0.6   | Linux            |
| ELK      |ELK/Kibana| 10.2.0.4   | Linux            |
 
### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jumpbox machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- 67.176.49.44
Machines within the network can only be accessed by the Jumpbox.

- My personal host machine is being used to access the ELK VM (IP: 67.176.49.44)

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes                 | 67.176.49.44         |
| Web1     | No                  | 10.0.0.4 & 10.0.0.5  |
| Web2     | No                  | 10.0.0.4 & 10.0.0.6  |
| ELK      | Yes (HTTP)          | 67.176.49.44         |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
-What is the main advantage of automating configuration with Ansible?_Playbooks allow for automated configuration of services across all machines within a network using that container. This means that all DVWA’s within the network can be configured at the same time instead of individually. 

The playbook implements the following tasks:
- Install docker.io
- Install python3-pip
- Install Docker module
- Download and launch docker elk container
- Enable service docker on boot

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance. 

gifted_lamport is the container being used.

![docker ps](https://user-images.githubusercontent.com/89494589/148151878-17317039-5a26-4756-9091-8cae0a351b84.png)


### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- Web1 (10.0.0.5), Web2 (10.0.0.6)

We have installed the following Beats on these machines:
- Filebeat and Metricbeat

These Beats allow us to collect the following information from each machine:
Filebeat monitors log files and log events. Metricbeat looks out for any information in the file system which has been manipulated and automatically sends it to Elasticsearch or similar tool for indexing and review.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the ansible configuration file to run the playbook.
- Update the ansible host file to include IP addresses of machines that beats will be deployed on.
- Run the playbook, and navigate to Web1 and Web2 to check that the installation worked as expected.

- The ansible playbook (activity1.yml) is in the ansible directory located in the /etc directory of the Jumpbox.
- The host file is located in the same ansible directory (-/etc/ansible/hosts) and needs to be updated to run on specific machines. Installation of the ELK machine and tools such as Filebeat must be dictated in the ansible configuration file.
- The URL to access Kibana is as follows: (ELK Public IP):5601/app/kibana. The current public IP for the ELK machine is 13.77.214.176


ansible-playbook install-elk.yml

dpkg -i
