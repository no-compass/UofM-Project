## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![Diagram](Diagrams/Network Map ElkStack.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the playbook (.yml) file may be used to install only certain pieces of it, such as Filebeat.

  The following ansible-playbooks are needed to create and install DVWA and the ELK-server
  * [my-playbook.yml](YML-Playbooks/my-playbook.yml) - used to install DVWA servers
  * [elk-playbook.yml](YML-Playbooks/elk-playbook.yml) - used to install ELK Server
    * [filebeat-playbook.yml](YML-Playbooks/filebeat-playbook.yml) - Used to install and configure Filebeat on Elk Server and DVWA servers
    * [metricbeat-playbook.yml](YML-Playbook) - Used to install and configure Metricbeat on Elk Server and DVWA servers

This document contains the following details:
- Description of the Topology
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


| Name       | Function   | IP Address | Operating System |
|------------|------------|------------|------------------|
| Jump Box   | Gateway    | 10.0.0.1   | Linux            |
| 1DVWA      | Web Server | 10.0.0.7   | Linux            |
| 2DVWA      | Web Server | 10.0.0.8   | Linux            |
| ELK Server | Monitoring | 10.1.0.9   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet.

Only the Jump Box Provisioner machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
* Personal IP Address

Machines within the network can only be accessed by SSH.
* The ELK-Server is only accessible by SSH from the JumpBox and via web access from Personal IP Address.

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

![docker-ps](Images/docker-ps.png)

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
- Copy the filebeat-config.yml and metricbeat-config.yml file to /etc/ansible/files.
- Update the configuration files to include the Private IP of the ELK-Server to the ElasticSearch and Kibana Sections of the Configuration File
- Run the playbook, and navigate to ELK-Server-PublicIP:5601/app/kibana to check that the installation worked as expected.

Which file is the playbook?
The playbook files are:
* [elk-playbook.yml](YML-Playbooks/elk-playbook.yml) - used to install ELK Server
  * [filebeat-playbook.yml](YML-Playbooks/filebeat-playbook.yml) - Used to install and configure Filebeat on Elk Server and DVWA servers
  * [metricbeat-playbook.yml](YML-Playbook) - Used to install and configure Metricbeat on Elk Server and DVWA servers

Where do you copy it?

/etc/ansible/

Which file do you update to make Ansible run the playbook on a specific machine?

/etc/ansible/hosts.cfg

How do I specify which machine to install the ELK server on versus which to install Filebeat on?

In /etc/ansible/hosts you tell it where you want eachto be installed ElkServers or FileBeat

Which URL do you navigate to in order to check that the ELK server is running?

http://publicip(elkserver):5601

### Commands needed to run the Anisble Configuration for the Elk-Server are:
1. ssh RedAdmin@JumpBox(PrivateIP)
2. sudo docker container list -a - Locate the ansible container
3. sudo docker start <name of container>(daisy_pain)
4. sudo docker attach <name of container>(daisy_pain)
5. cd /etc/ansible
6. ansible-playbook elk-playbook.yml (Installs and Configures ELK-Server)
7. cd /etc/ansible/
8. ansible-playbook beats-playbook.yml (Installs and Configures Beats)
9. Open a new browser on Personal Workstation, navigate to (ELK-Server-PublicIP:5601/app/kibana) - This will bring up Kibana Web Portal


### References
Filebeat: Lightweight Log Analysis &amp; Elasticsearch. (n.d.). Retrieved August 22, 2020, from https://www.elastic.co/beats/filebeat
Metricbeat: Lightweight Shipper for Metrics. (n.d.). Retrieved August 22, 2020, from https://www.elastic.co/beats/metricbeat