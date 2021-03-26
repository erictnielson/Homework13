## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

https://github.com/erictnielson/Homework13/tree/main/Diagrams

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, the filebeat-playbook.yml file may be used to install only certain pieces of it, such as Filebeat.

https://github.com/erictnielson/Homework13/blob/main/Ansible/filebeat-playbook

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly efficient, in addition to restricting access to the network.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the operating system and system logs.

The configuration details of each machine may be found below.

| Name       | Function                                      | IP Address | Operating System |
|------------|-----------------------------------------------|------------|------------------|
| Jump Box   | Secure, monitored zone to control access      | 10.0.0.5   | Linux            |
| Web-1      | Web Server                                    | 10.0.0.6   | Linux            |
| Web-2      | Web Server                                    | 10.0.0.7   | Linux            |
| ELK-Server | ELK Server (Elasticsearch, Log Stash, Kibana) | 10.1.0.4   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump Box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
71.10.76.35

Machines within the network can only be accessed by SSH from my laptop, 71.70.76.35.

A summary of the access policies in place can be found in the table below.

| Name       | Publicly Accessible | Allowed IP Addresses |
|------------|---------------------|----------------------|
| Jump Box   | Yes through SSH     | 71.70.76.35:8080     |
| Web-1      | No                  |                      |
| Web-2      | No                  |                      |
| ELK-Server | Yes, Port 5601      | 71.10.76.35:5601     |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because the process is configured once and can easily be copied to multiple new machines and we can be sure that no settings were modified other than those in the automatic configuration.  This makes troubleshooting much easier.

The playbook implements the following tasks:

-  Installs Docker.io
-  Installs pip3
-  Installs the Docker python module
-  Configures the system to use more memory
-  Downloads and rns the docker ELK container
-  Ensures that the Docker service runs at startup

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

https://github.com/erictnielson/Homework13/blob/main/Images/Docker.png

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
| Name  | IP Address |
|-------|------------|
| Web-1 | 10.0.0.6   |
| Web-2 | 10.0.0.7   |

We have installed the following Beats on these machines:
Filebeat and Metricbeat

These Beats allow us to collect the following information from each machine:

- Filebeat collects log files, allowing us to monitor system logs and events, making them searchable and able to be forwarded to other tools.  For example, Filebat will show us which computers accessed our system within a certain timeframe and from a certain country, allowing us to quickly diagnose when we may be attacked and where the attacks originate from

-  Metricbeat collects metrics from operating system and services that are running, allowing easier viewing of this information.  Foe example, Metricbeat allows us to see, in real time, when a system or service is being negatively impacted by a Denial of Service (DoS) attack 
  
### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the filebeat-config.yml file to /etc/ansible/files.
- Update the filebeat-config-yml file to so that after the word "hosts" (around line 1100) has the the correct IP address of your Jump Box (port :9200), username and password. Around line 1800, also change the host to be the correct IP address of your Jump box (port :5601) 
- Navigate back to /etc/ansible and run ansible-playbook filebeat-playbook.yml
- Run the playbook, open a web browser and go to <[External IP address of your Jump Box]/app/Kibana> to check that the installation worked as expected.
