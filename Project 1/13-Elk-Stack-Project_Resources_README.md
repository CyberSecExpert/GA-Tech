## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

Please refer to: Azure Network Topology Diagram.pdf

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment referenced above. Alternatively, select portions of the playbook files may be used to install only certain pieces of it, such as Filebeat.

  - filebeat-playbook.yml

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build

### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting inbound access to the network.
- The load balancer distributes the web requests load to the two web servers making their processing more efficient to maintain a 
  higher level of availability and responsiveness. The jump box machine is set up to minimize the open ports of the servers to
  minimize attack surface against potential hacking attacks.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the file systems of the VMs on the network, 
as well as watch system metrics, such as CPU usage; attempted SSH logins; sudo escalation failures; etc.
- Filebeat collects data about the file system.
- Metricbeat collects machine metrics, such as uptime.

The configuration details of each machine may be found below.

|    Name   |  Function  | IP Address | Operating System |
|-----------|------------|------------|------------------|
| Jump-Box  | Gateway    | 10.0.0.4   | Linux            |
| ELK-Server| Monitoring | 10.1.0.5   | Linux            |                  
| Web-1     | Web Server | 10.0.0.5   | Linux            |
| Web-2     | Web Server | 10.0.0.6   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump-Box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- 75.4.189.190

Machines within the network can only be accessed by:
- Jump-Box VM 10.0.0.4

A summary of the access policies in place can be found in the table below.

| Name      | Publicly Accessible | Allowed IP Addresses |
|-----------|---------------------|----------------------|
| Jump-Box  | Yes                 | 75.4.189.190         |
| ELK-Server| No                  | 10.0.0.1-254         |
| Web-1     | No                  | 10.0.0.1-254         |
| Web-2     | No                  | 10.0.0.1-254         |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- It simplifies and speeds up deployment, facilitates scaling and management of the servers and most of the taks the system administrator
does periodically.

The playbook implements the following tasks:
- Installs Docker
- Installs the Docker Python3-pip module
- Increases virtual memory
- Downloads and launches the Docker ELK container
- Publishes the ports that ELK runs on

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

- docker_ps_output.png  

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- Web-1 10.0.0.5
- Web-2 10.0.0.6

We have installed the following Beats on these machines:
- Filebeat
- Metricbeat

These Beats allow us to collect the following information from each machine:
- Filebeat: Filebeat detects changes to the filesystem. Specifically, we use it to collect web server logs.
- Metricbeat: Metricbeat detects changes in system metrics, such as CPU usage. We use it to detect SSH login 
  attempts, failed sudo escalations, and CPU/RAM statistics. 

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the filebeat-playbook.yml file to /etc/ansible/roles directory.
- Update the filebeat-config.yml file to include the ELK server's ip address.
- Run the playbook, and navigate to Filebeat installation page on the ELK server GUI to check that the installation worked as expected. (Step 5: Module Status and Check Data
  then scroll to the bottom and click on Verify Incoming Data)

_TODO: Answer the following questions to fill in the blanks:_ 
- _Which file is the playbook? filebeat-playbook.yml Where do you copy it? /etc/ansible/roles
- _Which file do you update to make Ansible run the playbook on a specific machine? The 'filebeat-config.yml' file
-  How do I specify which machine to install the ELK server on versus which to install Filebeat on? 'hosts' file vs 'filebeat-playbook.yml' file 
- _Which URL do you navigate to in order to check that the ELK server is running? http://[ELK.VM.IP]:5601/app/kibana alternatively use the curl command.


