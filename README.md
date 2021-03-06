# CyberSecurityProject1
CyberSecurityClassProject1


Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

[Network Diagram](https://github.com/bradygg/CyberSecurityProject1/blob/fa31942d10bebea1a372806251976d18f131aac7/Diagrams/networkdiagram.png)


These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the playbook file may be used to install only certain pieces of it, such as Filebeat.

[filebeat-config.yml](https://github.com/bradygg/CyberSecurityProject1/blob/903ab4f17d34655866a03cdb4b58813d657afd3a/Ansible/filebeat-config.yml)

[elk.yml](https://github.com/bradygg/CyberSecurityProject1/blob/903ab4f17d34655866a03cdb4b58813d657afd3a/Ansible/elk.yml)

[filebeat-playbook.yml](https://github.com/bradygg/CyberSecurityProject1/blob/903ab4f17d34655866a03cdb4b58813d657afd3a/Ansible/filebeat-playbook.yml)

[metricbeat-config.yml](https://github.com/bradygg/CyberSecurityProject1/blob/903ab4f17d34655866a03cdb4b58813d657afd3a/Ansible/metricbeat-config.yml)

[metricbeat-playbook.yml](https://github.com/bradygg/CyberSecurityProject1/blob/903ab4f17d34655866a03cdb4b58813d657afd3a/Ansible/metricbeat-playbook.yml)

[pentest.yml](https://github.com/bradygg/CyberSecurityProject1/blob/903ab4f17d34655866a03cdb4b58813d657afd3a/Ansible/pentest.yml)

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
What aspect of security do load balancers protect? What is the advantage of a jump box?
- Defend against DSoS attacks. Load balancers can guard and protect against unauthorized access. They can request specific credentials prior to access. In this environment Load balancers help with web traffic
- Remotely gain access to another machine on a network. Used to manage devices in separate security zones as well

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the files and data and system logs.
What does Filebeat watch for?
- Watches log files that you identify and sends them to elasticsearch/Logstash for proper filing
What does Metricbeat record?
-Records metrics and statistical data and then send them to the output specified though elasticsearch/Logstash

The configuration details of each machine may be found below.

| Name               | Function | IP Address Public/Private | Operation System |
|--------------------|----------|---------------------------|------------------|
| JumpBoxProvisioner | Gateway  | 13.67.211.88/10.0.0.7     | Linux            |
| Web-1              | Server   | 13.89.7.78/10.0.0.8       | Linux            |
| Web-2              | Server   | 13.89.7.78/10.0.0.6       | Linux            |
| ELK-Server         | Server   | 52.147.197.240/10.2.0.4   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the JumpBoxProvisioner machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
Add whitelisted IP addresses
-Local Host IP Address

Machines within the network can only be accessed by JumpBoxProvisioner.
Which machine did you allow to access your ELK VM? What was its IP address?
JumpBoxProvisioner 13.67.211.88

A summary of the access policies in place can be found in the table below.

| Name               | Publicly Accessible | Allowed IP                                           | Port |
|--------------------|---------------------|------------------------------------------------------|------|
| JumpBoxProvisioner | Yes                 | Host IP                                              | 22   |
| Web-1 (VM)         | No                  | JumpBoxProvisioner via Docker Container              |      |
| Web-2 (VM)         | No                  | JumpBoxProvisioner via Docker Container              |      |
| LoadBalancer       | Yes                 | Host IP                                              | 80   |
| ELK-Server         | Yes                 | Host IP                                              | 5601 |
| ELK-Server         | No                  | Peering Connection between existing virtual networks |      |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
What is the main advantage of automating configuration with Ansible?

-Anisble automation is a simple and fast way of installing/deploying resources or programs in cloud environments for multiple machines massively reducing risks of errors by deploying manually.

The playbook implements the following tasks:
In 3-5 bullets, explain the steps of the ELK installation play. E.g., install Docker; download image; etc._

*SSH into JumpBoxProvioner (ssh azuresuer@13.67.211.88)

*start/attached to ansible docker (sudo docker start  relaxed_goldwasser) & (sudo docker attach relaxed_golnwasser)

*Cd???d into /etc/ansible and created the ELK playbook (nano elk.yml)

*Ran Elk playbook in the directory (ansible playbook elk.yml)

*Finally SSH into ELK-Server to verify up an running ( ssh azureuser@10.2.0.4)


The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![Docker ps output](https://github.com/bradygg/CyberSecurityProject1/blob/0da7f857439f05fdef3dd4133423cdecfa9938a7/Images/SudodockerPS.jpg)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
Web-1 10.0.0.8

Web-2 10.0.0.6

We have installed the following Beats on these machines:
Specify which Beats you successfully installed_

-Filebeat and Metricbeat were both installed successfully on Web-1 & Web-2


These Beats allow us to collect the following information from each machine:
In 1-2 sentences, explain what kind of data each beat collects, and provide 1 example of what you expect to see. E.g., `Winlogbeat` collects Windows logs, which we use to track user logon events, etc._
-Filebeat is used for collecting log files on remote machines
Apache, logstash, aws cloud watch files are examples of files that can be generated and stored by filebeat files

-Metricbeat collects machine metrics and monitors systems status
Docker metrics is an example and also can show health and usage



### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the filebeat-config.yml file to /etc/ansible.
- Update the filebeat-config.yml file to include ELK private IP 10.2.0.4 in lines 1106 and 1806
- Run the playbook, and navigate to http://52.147.197.240:5601 (ELK-Server Public IP) to check that the installation worked as expected.

- Copy the metricbeat-config.yml file to /etc/ansible.
- Update the metricbeat-config.yml file to include ELK private IP 10.2.0.4 in lines 62 and 96
- Run the playbook, and navigate to http://52.147.197.240:5601 (ELK-Server Public IP) to check that the installation worked as expected.

Answer the following questions to fill in the blanks:_
- _Which file is the playbook? Where do you copy it?_

ELK: elk.yml copy file to /etc/ansible/elk.yml

Filebeat: filebeat-playbook.yml copy file to /etc/ansible/filebeat-playbook.yml

Metricbeat: metricbeat-playbook.yml copy file to /etc/ansible/metricbeat-playbook.yml



- _Which file do you update to make Ansible run the playbook on a specific machine? 

You would have to update the hosts file with the new machines private IP within /etc/ansible/hosts

- How do I specify which machine to install the ELK server on versus which to install Filebeat on?_

There has to be two separate groups set up in the etc/ansible/hosts. One group being webservers which has the Web VMs Private IPs where I install filebeat to. The other group being elk and having the ELK-Server and its private IP

![Host updates](https://github.com/bradygg/CyberSecurityProject1/blob/0da7f857439f05fdef3dd4133423cdecfa9938a7/Images/ElkServeraddon.jpg)

- _Which URL do you navigate to in order to check that the ELK server is running?

http://52.147.197.240:5601

