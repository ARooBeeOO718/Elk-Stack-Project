# Elk-Stack-Project
This is my project demonstrating the creation of virtual networks and their supportive machines and scripts as well as a diagram showing connections to and from firewalls and subnetworks.
## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![virtual network](Images/https://app.diagrams.net/#G1hqXQgKZczenmBvu56Qo5u4FECKrIiNyo)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the Ansible playbook file may be used to install only certain pieces of it, such as Filebeat.

  
  - ![Filebeat Playbook] (https://github.com/ARooBeeOO718/Elk-Stack-Project/blob/main/Ansible/filebeat-playbook.yml) to install and configure Filebeat on the target machines.
  - ![Elk Play] (https://github.com/ARooBeeOO718/Elk-Stack-Project/blob/main/Ansible/elk-play.yml) to install and configure the ELK server
  - ![Metricbeat Playbook] (https://github.com/ARooBeeOO718/Elk-Stack-Project/blob/main/Ansible/metricbeat-playbook.yml) to install and configure Metricbeat on the target machines.
  

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
- Load balancers protect the system from DDoS attacks as it shifts attacking traffic. The advantage of having a jump box is that it gives access to the user from a
- single node that can be secured and monitored. 

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the VM metrics and system logs.
- Filebeat monitors system logs on machines.
- Metricbeat records metrics from the operating system and from services running on the server. Metricbeat takes the metrics and statistics that it collects and ships them 
- to the output that you specify such as Elasticsearch or Logstash.

The configuration details of each machine may be found below:
| Name                 | Function    | IP Address | Operating System |
|----------------------|-------------|------------|------------------|
| Jump-Box-Provisioner | Gateway     | 10.0.0.4   | Linux(Ubuntu)    |
| Web-1                | DVWA Server | 10.0.0.5   | Linux(Ubuntu)    |
| Web-2                | DVWA Server | 10.0.0.6   | Linux(Ubuntu)    |
| Web-3                | DVWA Server | 10.0.0.8   | Linux(Ubuntu)    |
| Elk-Stack-VM         | Elk Stack   | 10.1.0.4   | Linux(Ubuntu)    |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump-Box-Provisioner machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- 50.39.145.XXX(Withheld for security purposes)

Machines within the network can only be accessed by the Jump Box and which has the IP address of 10.0.0.4.

A summary of the access policies in place can be found in the table below.

| Name                 | Publicly Accessible  | Allowed IP Addresses  |
|----------------------|----------------------|-----------------------|
| Jump-Box-Provisioner | Yes                  | 50.39.145.XXX         |
| Web-1                | No                   | 10.1.0.4              |
| Web-2                | No                   | 10.1.0.4              |
| Web-3                | No                   | 10.1.0.4              |
| Elk-Stack-VM         | No                   | 10.1.0.4              |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because it is flexible, meaning that
you can orchestrate the entire application environment no matter where it may be deployed. You do not need to install any other software of firewall ports on the client 
systems you want to automate. Another big advantage is that it reduces the chances of human error.

The playbook implements the following tasks:
- https://github.com/ARooBeeOO718/Elk-Stack-Project/blob/main/Ansible/elk-play.yml
. Install docker.io package using apt
. Install python3-pip package manager using apt
. Install the docker module using pip
. Configure the VM to use more memory using sysctl module
. Download and launch the docker container for Elk Stack
- https://github.com/ARooBeeOO718/Elk-Stack-Project/blob/main/Ansible/filebeat-playbook.yml 
. Download and install Filebeat
. Copy configuration for Filebeat
. Enable Filebeat system module
. Setup Filebeat  
. Start and enable Filebeat service

- https://github.com/ARooBeeOO718/Elk-Stack-Project/blob/main/Ansible/metricbeat-playbook.yml
. Download and install Metricbeat
. Copy Metricbeat configuration
. Enable Metricbeat docker module
. Setup Metricbeat 
. Start and enable Metricbeat service 

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![C:\Users\arubi\OneDrive\Documents\Project1screenshots](Images/Project1screenshots.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- Web-1 IP Address: 10.0.0.5
- Web-2 IP Address: 10.0.0.6
- Web-3 IP Address: 10.0.0.8

We have installed the following Beats on these machines:
- Filebeat
- Metricbeat

These Beats allow us to collect the following information from each machine:
- Filebeat monitors log files or locations that you specify, collecting log events, and forwards them to either Elasticsearch or Logstash. It allows us to view successful
or failed processes. 

-Metricbeat collects metric information on each system, allowing us to view network I/O, CPU usage, and memory pressure.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the three playbook files (elk-play.yml, filebeat-playbook.yml, and metricbeat-playbook.yml) to the /etc/ansible/roles directory in your control node.
- Update the /etc/ansible/hosts file. You will need to include a group called elk which contain the IP address of the server you wish to install the ELK stack on.
- Run the playbook, and navigate to http://[Public IP of ELK SERVER:5601] to check that the installation worked as expected.

- The file ending in .yml indicates that this is a playbook file. You copy it in roles directory so you can later run a command to update a file to make Ansible run the playbook.
- That file that you update to make Ansible run is the hosts file with the appropriate configuration including IP addresses of machines you want to run. 
- You specify which machine to install the elk server by running the command "ansible-playbook /etc/ansible/elk-play.yml"
- Then you would run "ansible-playbook /etc/ansible/roles/filebeat-playbook.yml"
- Run the Metricbeat installation play book "ansible-playbook /etc/ansible/roles/metricbeat-playbook.yml"
- You navigate to the URL http://[Public IP of ELK SERVER:5601] to check that the ELK server is running.
