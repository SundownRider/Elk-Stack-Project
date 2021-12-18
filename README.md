# Elk-Stack-Project

## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![Azure Diagram](https://github.com/SundownRider/Elk-Stack-Project/blob/main/Diagrams/Azure_Network.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the configuration file may be used to install only certain pieces of it, such as Filebeat.

![Filebeat Configuration File](https://github.com/SundownRider/Elk-Stack-Project/blob/main/Ansible/filebeat-configuration.yml)  
![Filebeat Playbook File](https://github.com/SundownRider/Elk-Stack-Project/blob/main/Ansible/filebeat-playbook.yml)

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly accessible, in addition to preventing downtime to the network.  
Load balancers protect the Availability aspect of the CIA triad by routing traffic equally among each web server.   
One advantage of implementing a Jump Box is the ability to deploy ansible and effeciently manage web servers.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes in the server logs and system metrics.  
Filebeat: Filebeat gathers system logs and sends them to a specified output (Logstash or Elasticsearch).        
Metricbeat: Metricbeat periodically records system metrics and statistics and sends them to a specified output (Logstash or Elasticsearch).

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
|Jump Box  |Gateway   | 10.0.0.4   | Linux            |
|Web-1     |Webserver | 10.0.0.5   | Linux            |
|Web-2     |Webserver | 10.0.0.6   | Linux            |
|Elk-Server|Monitoring| 10.2.0.4   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Elk-Server machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:

74.192.25.186

Machines within the network can only be accessed via Secure Shell (SSH).
I allowed the Ansible container on the Jump-Box machine to access the Elk-Server machine on the back-end.  

Jump-Box/Ansible IP: 10.0.0.4 (Internal)  

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
|Jump Box  | No                  |74.192.25.186         |
|Web-1     | No                  |74.192.25.186 10.0.0.4|
|Web-2     | No                  |74.192.25.186 10.0.0.4|
|Elk-Server| Yes                 |74.192.25.186 10.0.0.4|

### Elk Configuration

Ansible was used to automate configuration of the ELK machine.

One significant advantage of automating the configuration with Ansible was the simplicity of the installation. I was able to minimize the risk of misconfiguration through the use of Ansible.

The playbook implements the following tasks:  
1. Install the Docker.io Package  
2. Install Python3 (pip3)  
3. Install The Docker Module Using Python3 (pip3)  
4. Extend The Amount Of Memory Allocated To Docker  
5. Download and Launch An Elk Conatiner Using Docker

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![Elk_Docker_PS](https://github.com/SundownRider/Elk-Stack-Project/blob/main/Images/Docker_PS.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:

Web-1: 10.0.0.5  
Web-2: 10.0.0.6

We have installed the following Beats on these machines:  

1. Filebeat    
2. Metricbeat

These Beats allow us to collect the following information from each machine:

Filebeat collects system logs which can be used to monitor network activity for any suspicious activity. For example, if a malicious user were to gain unauthorized access to the network, a log of this user's activity would be collected by filebeat.    

Metricbeat collects system metrics which can be used to identify performance issues on a specific server or on the entire network.  

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the ![install-elk.yml](https://github.com/SundownRider/Elk-Stack-Project/blob/main/Ansible/install-elk.yml) file to the /etc/ansible directory.
- Update the /etc/ansible/hosts file to include the IP addresses of the webservers that you would like to install ELK on and the IP address of the ELK virtual machine  
![Ansible Hosts](https://github.com/SundownRider/Elk-Stack-Project/blob/main/Images/Hosts.png)  
- Run the playbook, and navigate to http://[Elk-Server External IP]:5601/app/kibana to check that the installation worked as expected.

Note: An example installation write up can be found ![here](https://github.com/SundownRider/Elk-Stack-Project/blob/main/WriteUp.txt)
