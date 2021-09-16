## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

https://github.com/prashantkhopkar/cyberbootcamp2021/blob/main/Images/Network%20Topplogy.PNG
![image](https://user-images.githubusercontent.com/83466220/133692941-f4f87d1b-f262-4f8b-bb08-514d54ee6b5b.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the filebeat-playbook.yml file may be used to install only certain pieces of it, such as Filebeat.

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
- A loadbalancer is meant to serve a specific point of access for a service that is served by multiple machines. This allows high availability models to function properly_
- A jumpbox or bastion server acts as a gateway to gain entry into a remote network. Many times the primary mode of access is ssh and without the key access is forbidden.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the logfiles and system resources.
- Filebeat is meant primarily to watch for system logs and forward any changes to the Elasticsearch Host
- Metricbeat is used for gathering metrics and system resources usage for display in Elasticsearch

The configuration details of each machine may be found below.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway 		   | 10.0.0.4         | Ubuntu 20.04.3   |
| Web1     | Web Server            | 10.0.0.5         | Ubuntu 20.04.3   |
| Web2 	   | Web Server            | 10.0.0.6         | Ubuntu 20.04.3   |
| ELK      | ElasticSearch Stack   | 10.1.0.4         | Ubuntu 20.04.3   |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the jumpbox machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
45.26.60.195

Machines within the network can only be accessed by jumpbox.
Public IP: 104.42.32.214
Private IP: 10.0.0.4

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses         |
|----------|---------------------|------------------------------|
| Jump Box | Yes-SSH-Port 22     | 45.26.60.195          	|
| Web1     | No                  | Web Load Bal: 13.64.51.202   |
| Web2     | No                  | Web Load Bal: 13.64.51.202   |
| Load Bal | HTTP-80-Yes         | *                            |
| ELK      | Kibana-5601-Yes     | *                            |
| ELK      | HTTP API-9200-Yes   | 10.0.0.0/16                  |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
Allows for full automation of a specific server and reduces configuration errors. 

The playbook implements the following tasks:
- Install Docker: Installs the core docker code to the remote server_
- Install Phython3_pip: Pip is an installation module that allows for additional docker modules to be installed easier
- Docker module: Tells the previous Pip module to install the necessary docker component modules
- Increase memory/Use more memory: A common issue with the ELK docker image is less memory. Helps fix the issue.
- Download and launch ELK container: This downloads the ELK docker container and initializes it with the specified parts being published.

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

https://github.com/prashantkhopkar/cyberbootcamp2021/blob/main/Images/ELK%20Container.PNG
![image](https://user-images.githubusercontent.com/83466220/133693008-f8cf8ddc-4781-4169-885d-d2c78dd253b8.png)


### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- 10.0.0.5
- 10.0.0.6

We have installed the following Beats on these machines:
- Filebeats
- Metricbeats

Installed on Web 1 and Web 2
These Beats allow us to collect the following information from each machine:
- Filebeats collects system type events such as logins to see who is actively logging into the system.

https://github.com/prashantkhopkar/cyberbootcamp2021/blob/main/Images/FielBeats%20Dashboard%20Example.png
![image](https://user-images.githubusercontent.com/83466220/133693043-014ac2e3-09bd-41e7-94ad-f6b991f7c9d6.png)

- Metricbeats collects useful information about the container, cpu, disk, memory and network.

https://github.com/prashantkhopkar/cyberbootcamp2021/blob/main/Images/MetricBeat%20Dashboard%20Example.png
![image](https://user-images.githubusercontent.com/83466220/133693061-fccdc300-5777-49ca-94b1-1eedf1090180.png)

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the elk_install.yml file to /etc/ansible/roles/ansibleelkserverplaybook.yml.
- Update the hosts file to include the elk attribute [elkservers] and include destination ip of the ELK server directly below
https://github.com/prashantkhopkar/cyberbootcamp2021/blob/main/Images/Update%20Hosts%20File%20with%20Server%20Info_1.png
![image](https://user-images.githubusercontent.com/83466220/133693084-3bb1f13d-7562-4138-a426-91733566b174.png)

https://github.com/prashantkhopkar/cyberbootcamp2021/blob/main/Images/Update%20Hosts%20File%20with%20Server%20Info_2.png
![image](https://user-images.githubusercontent.com/83466220/133693106-82da6657-b32e-420d-b632-cc8522cbb52f.png)

- Run the playbook, and navigate to http://13.67.229.27: 5601/app/kibana#/home to check that the installation worked as expected.

https://github.com/prashantkhopkar/cyberbootcamp2021/blob/main/Images/Kibana%20Picture.png
![image](https://user-images.githubusercontent.com/83466220/133693124-1b058c98-5181-4c5c-a0a3-ad86a1b901f5.png)

1. On the jumpbox run the following command to get the playbook:
curl https://github.com/prashantkhopkar/cyberbootcamp2021/blob/main/Ansible/ansibleelkserverplaybook.yml

2. Edit the hosts file in /etc/ansible and add the details from the screen shot and update your ip address:
include link to the images

https://github.com/prashantkhopkar/cyberbootcamp2021/blob/main/Images/Update%20Hosts%20File%20with%20Server%20Info_2.png
![image](https://user-images.githubusercontent.com/83466220/133693157-f2e0c3ec-dcc6-4e26-a0fa-9f4485f36e4b.png)

3.To run the Playbook: ansible-playbook
/etc/ansible/roles/anisbleelkserverplaybook.yml

4.To check if installation is successful navigate via browser the following http://13.67.229.27:5601/app/kibana#/home

https://github.com/prashantkhopkar/cyberbootcamp2021/blob/main/Images/Kibana%20Picture.png
![image](https://user-images.githubusercontent.com/83466220/133693187-0c26205e-2745-46c7-8dd2-066506e22544.png)

5. Installing Filebeats
a. Download the playbook with the following command and save to the /etc/ansible/roles
curl https://github.com/prashantkhopkar/cyberbootcamp2021/blob/main/Ansible/filebeat-playbook.yml

b. Run the playbook with ansible-playbook command
/etc/ansible/roles/filebeat_playbook.yml

c. Successful installation and navigating to Kibana via the link mentioned above

https://github.com/prashantkhopkar/cyberbootcamp2021/blob/main/Images/FielBeats%20Dashboard%20Example.png
![image](https://user-images.githubusercontent.com/83466220/133693213-1d30a1b6-2f52-4dc0-8a45-041125848af5.png)

6. Installing metricbeats
a. Download the playbook with the following command and download and save to the /etc/ansible/roles
curl https://github.com/prashantkhopkar/cyberbootcamp2021/blob/main/Ansible/metricbeatplaybook.yml
b. Run the playbook with ansible-playbook
/etc/ansible/roles/metricbeat_playbook.yml
c. Successful installation and navigating to Kibana via the link mentioned above

https://github.com/prashantkhopkar/cyberbootcamp2021/blob/main/Images/MetricBeat%20Module%20Status%20Picture.png
![image](https://user-images.githubusercontent.com/83466220/133693248-10f176bb-dec3-4d56-ac06-9af7c2e39673.png)

https://github.com/prashantkhopkar/cyberbootcamp2021/blob/main/Images/Metricbeats%20Dashboard%20Picture%202.png
![image](https://user-images.githubusercontent.com/83466220/133693267-ec3b78c4-20dd-4f4b-976f-bd7e405b78b2.png)


