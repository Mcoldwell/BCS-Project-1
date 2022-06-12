## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![TODO: Update the path with the name of your diagram](Images/diagram_filename.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the .yml and config file may be used to install only certain pieces of it, such as Filebeat.

  - Ansible Playbook
  - Ansible Hosts
  - Ansible Configuration
  - Ansible ELK Installation and VM Configuration
  - Ansible Filebeat Playbook
  - Ansible Filebeat Config file
  - Ansible Metricbeat Playbook
  - Ansible Metricbeat Config file

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly avaliable, in addition to restricting unauthorised access to the network.
- _TODO: What aspect of security do load balancers protect? What is the advantage of a jump box?
Load balancers protect the availabiltiy, web security and webtraffic of a network.
Load balancers also provide the advantage of security and access control as well as network segmentation to the network.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the data and system logs.
- _TODO: What does Filebeat watch for?_
Filebeat watches the locations or logs that are specified it then collects the log events and sends them to elasticsearch or logstash.
- _TODO: What does Metricbeat record?_
Metricbeat records the statictics and metrics and sends them to an output that is specified such as elasticsearch or logstash


The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name          | Function            | IP Address                 | Operating System |
|---------------|---------------------|----------------------------|------------------|
| Jump Box      | Gateway             | 10.0.0.4/ 20.53.252.160    | Linux            |
| Web-1         | Web Server          | 10.0.0.5                   | Linux            |
| Web-2         | Web Server          | 10.0.0.6                   | Linux            |
| ELK-Stack-VM1 | ElasticSearch Stack | 10.1.0.4 / 52.243.92.135   | Linux            |
| Load Balancer | loadpool            | Static External IP         | Linux            |
| Workstation   | Access control      | Public IP                  | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jumpbox machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses: 103.217.166.177


Machines within the network can only be accessed by docker container.
- _TODO: Which machine did you allow to access your ELK VM? What was its IP address?_
The jump box private IP 10.0.0.4 through SSH port 22
The workstations public IP through port TCP 5601

A summary of the access policies in place can be found in the table below.

| Name          | Publicly Accessible | Allowed IP Addresses                |
|---------------|---------------------|-------------------------------------|
| Jump Box      | No                  | workstation public IP on SSH 22     |
| Web-1         | No                  | 10.0.0.4 on SSH 22                  |
| Web-2         | No                  | 10.0.0.4 on SSH 22                  |
| ELK-Stack-VM1 | No                  | workstaiton public IP using TCP 5601|
| Load Balancer | No                  | workstation public IP using HTTP 80 |


### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- _TODO: What is the main advantage of automating configuration with Ansible?_
This is advantageous because there is no need to spend time setting up systems or writing code to automate the systems all tasks are completed through the Ansible playbook.

The playbook implements the following tasks:
- _TODO: In 3-5 bullets, explain the steps of the ELK installation play. E.g., install Docker; download image; etc._
- install the docker.io apt
- install the python3-pip
- increase virtual memory
- download and launch a docker elk container
- enable the docker service to start on boot.

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![TODO: Update the path with the name of your screenshot of docker ps output](Images/docker_ps_output.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- _TODO: List the IP addresses of the machines you are monitoring_
- Web-1 via 10.0.0.5
- Web-2 via 10.0.0.6

We have installed the following Beats on these machines:
- _TODO: Specify which Beats you successfully installed_
Elk Server, Web-1 and Web-2

These Beats allow us to collect the following information from each machine:
- _TODO: In 1-2 sentences, explain what kind of data each beat collects, and provide 1 example of what you expect to see. E.g., `Winlogbeat` collects Windows logs, which we use to track user logon events, etc._
- Filebeat: Log events.
- Metricbeat: system and metric statistics.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the ansible.cfg file to your elk machine.
- Update the ansible.cfg file to include remote_user = azureuser
- Run the playbook, and navigate to /etc/ansible to check that the installation worked as expected.

_TODO: Answer the following questions to fill in the blanks:_
- _Which file is the playbook? Where do you copy it?_
the ansible play book is my-playbook.yml
- _Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?_
hosts file placing the following string under the [elk] 10.1.0.4 ansible_python_interpreter=/usr/bin/python3
- _Which URL do you navigate to in order to check that the ELK server is running?
http://[your.VM.IP]:5601/app/kibana

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._