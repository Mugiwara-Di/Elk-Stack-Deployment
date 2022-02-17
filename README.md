## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![Diagram](Diagram/Elk-Diagram.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the YAML file may be used to install only certain pieces of it, such as Filebeat.

  - [Elk Playbook](https://github.com/TooBigBaba/Elk-Stack-Deployment/blob/main/Ansible/install-elk.yml) 
  - [Filebeat Playbook](https://github.com/TooBigBaba/Elk-Stack-Deployment/blob/main/Ansible/filebeat-playbook.yml)
  - [Metricbeat Playbook](https://github.com/TooBigBaba/Elk-Stack-Deployment/blob/main/Ansible/Metricbeat-Playbook.yml)

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting in-bound access to the network.
- A load balancer distributes traffic from clients across multiple servers without the clients having to understand how many servers are in use or how they are configured. 

- A secure jump box is an excellent out-of-band (OOB) remote access method for system administrators. It ensures that your network has 24x7x365 support and is a reasonable solution when some of your users either have no direct office or data center access.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the jumpbox and system network.
- Filebeat watches for changes made to files on a machine.
- Metrickbeat collects metrics from the operating system and from services running on the server.

The configuration details of each machine may be found below.

| Name       | Function   | IP Address | Operating System |
|------------|------------|------------|------------------|
| Jump-Box   | Gateway    | 10.0.0.7   | Linux            |
| Web-1      | Webserver  | 10.0.0.8   | Linux            |
| Web-2      | Webserver  | 10.0.0.9   | Linux            |
| Web-3      | Webserver  | 10.0.0.10  | Linux            |
| Elk-Server | Monitoring | 10.1.0.4   | Linux            |


### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the jumpbox provisioner machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- My IP address

Machines within the network can only be accessed by jump box provisioner.
- Web-1
- Web-2
- Web-3

A summary of the access policies in place can be found in the table below.

| Name       | Publicly Accessible | Allowed IP Addresses |
|------------|---------------------|----------------------|
| Jump-Box   | Yes                 | My IP address        |
| Web-1      | No                  | 10.1.0.4             |
| Web-2      | No                  | 10.1.0.4             |
| Web-3      | No                  | 10.1.0.4             |
| Elk-Server | No                  | 10.1.0.4             |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- Very simple to set up and use.
- Easily accesible and customizable based on your needs.
- Anisble is an open-source tool so it's free.
- You don't have to install any other software of firewall ports making it angentless.
- It takes up no space on your server allowing for more room for applications.

The playbook implements the following tasks:
- Install docker.io
- Install pip3
- Install Docker python module
- Increase virtual memory
- Dowload and launch a docker

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![Docker](Images/Docker.PNG)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:

| Name  | IP Address |
|-------|------------|
| Web-1 | 10.0.0.8   |
| Web-2 | 10.0.0.9   |
| Web-3 | 10.0.0.10  |

We have installed the following Beats on these machines:
- Microbeats

These Beats allow us to collect the following information from each machine:
- Filebeat monitors the log files or locations specified, collects log events, and forwards them for indexing.
- Metricbeat collects metric data from your target servers, this could be operating system metrics such as CPU or memory or data related to services running on the server.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the playbook file to Ansible control node.
- Update the host file to include the machine(s) to install the Elk server on.
- Run the playbook, and navigate to Kibana (http://[your.VM.IP]:5601/app/kibana) to check that the installation worked as expected.

Notable information
- The playbook can be found in the /etc/ansible directory
- You will nede to update the host file in this directory to make Ansible run the playbook on a specific machine. Withn the host file you will be able to add or remove machines from the specifed group. If the host file has the correct specifed machine, they playbook will automaticily run and install what needs to be installed on the specifed IP.
- Navigate to (http://[your.VM.IP]:5601/app/kibana) to make sure the Elk server is running.

Commands
- Download playbook:
 `cd /etc/ansible`
 `ansible-playbook Metricbeat-Playbook.yml`
 `ansible-playbook Filebeat-playbook.yml`

- Edit host file:
``````
root@9bf2ebe127ae:/etc/ansible# cd /etc/ansible
root@9bf2ebe127ae:/etc/ansible# nano hosts
 
 [webservers]
 10.0.0.8
 10.0.0.9
 10.0.0.10

 [elk]
 10.1.0.4
```````
