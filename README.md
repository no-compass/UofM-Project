## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

https://github.com/no-compass/UofM-Project/tree/main/Diagrams

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the yml file may be used to install only certain pieces of it, such as Filebeat.

  - _TODO: Enter the playbook file._

This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

-Load balancing ensures that the application will be highly available, in addition to restricting Access to the network.
-The load balancer defends against denial-of-service (DDoS) attacks.
-Load balancers conduct health checks on servers to ensure they can handle requests.
-The Jump Box Limits attack surface allowong only one ip address access.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the file systems and system metrics.
- Filebeat monitors the log files or collects log events, and forwards them either to Elasticsearch or Logstash for indexing.
- Metricbeat takes the metrics and statistics that it collects and sends them to Elasticsearch or Logstash

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.



### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump Box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
197.44.39.33

Machines within the network can only be accessed by each other.
- The ELK VM has traffic sent to it from 1Dvwa and 2DVWA

A summary of the access policies in place can be found in the table below.

| Name       | Function   | IP Address | Operating System |
|------------|------------|------------|------------------|
| Jump Box   | Gateway    | 10.0.0.1   | Linux            |
| 1DVWA      | Web Server | 10.0.0.7   | Linux            |
| 2DVWA      | Web Server | 10.0.0.8   | Linux            |
| ELK Server | Monitoring | 10.1.0.9   | Linux            |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
-Reduced errors and time savings.

The playbook implements the following tasks:
- Install docker.io
- Install pip3
- Install Docker python module
- Use more memory
- Download and launch a docker elk container

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![TODO: Update the path with the name of your screenshot of docker ps output](Images/docker_ps_output.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- 1DVWA 10.0.0.7
- 2DVWA 10.0.0.8

We have installed the following Beats on these machines:
-Filebeat
-Metricbeat
-Packetbeat

These Beats allow us to collect the following information from each machine:
-Filebeat: Filebeat detects changes to the filesystem. (Apache logs)
Metricbeat: Metricbeat detects changes in system metrics CPU, RAM statistics and SSH login attempts, failed sudo escalations.
Packetbeat: Packetbeat collects packets that pass through the NIC. 

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the playbook.yml file to _____.
- Update the playbook.yml file to include...
- Run the playbook, and navigate to ____ to check that the installation worked as expected.

_TODO: Answer the following questions to fill in the blanks:_
- _Which file is the playbook? Where do you copy it?_
- _Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?_
- _Which URL do you navigate to in order to check that the ELK server is running?

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._
