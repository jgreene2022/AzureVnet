# AzureVnet
Creating a virtual network using azure
## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![redteamvnet](https://user-images.githubusercontent.com/98893750/169672466-600cccff-0708-489d-ba3c-85707af4c33c.jpg)


These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the file may be used to install only certain pieces of it, such as Filebeat.

  - metricbeat-playbook.yml
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

Load balancing ensures that the application will be highly secure, in addition to restricting access to the network.
- In addition to security load balancers assist in the access of availablity to the network? The jump box also give us a security advantage to monitor/controll access of our virtual network.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the data and system.
- Filebeat is a lightweight shipper for forwarding and centralizing log data.
- Metricbeat takes the metrics and statistics that it collects and ships them to the output that you specify, such as Elasticsearch or Logstash.

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name                 | Function | IP Address | Operating System |
|----------------------|----------|------------|------------------|
| Jump Box Provisioner | Gateway  | 10.0.0.1   | Linux            |
| Web-1 VM             | Web Server  | 10.0.0.4   | Linux            |
| Web-2 VM             | Web Server  | 10.0.0.5   | Linux            |
| Elk Server           | Database for Network Security Monitoring  | 10.1.0.4   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump-Box-Provisoner machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- 20.213.146.248

Machines within the network can only be accessed by SSH (port 22) and HTTP (port 80).
- _Jump-Box Provisoner can access the ELK server from public IP address 20.213.146.248 

A summary of the access policies in place can be found in the table below.

| Name                 | Publicly Accessible | Allowed IP Addresses      |
|----------------------|---------------------|---------------------------|
| Jump Box Provisioner |          NO         |       20.213.146.248      |
| Web-1 VM             |         YES         |          10.0.0.4         |
| Web-2 VM             |         YES         |          10.0.0.5         |
| Elk Server           |          NO         | 20.212.201.205 / 10.1.0.4 |


### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because we have
created a code that contains the configuration of a server. That code can be version controlled and easily audited. The main advantage
of automating configuration with Ansible is the abilty to install software and change configuration files in thousands of servers
within a few minutes.

The playbook implements the following tasks:

- Install the docker.io downloads the software package from the Docker engine used for running containers.
- Install python-3 pip downloads the software packages used to install Python software.
- Install Docker modules initiates the python client for Docker which is required by Ansible.

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![docker-ps](https://user-images.githubusercontent.com/98893750/169672480-b6adaebd-daef-4cc9-bf03-72b75f7748e7.jpg)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- Web-1 10.0.0.4

-Web-2  10.0.0.5

We have installed the following Beats on these machines:
- _ Filebeat and Metricbeat

These Beats allow us to collect the following information from each machine:

-The File beat module collects and parses logs created by the system logging service. You will see sylog events, hostnames, and processes.
-The Metricbeat module collects CPU, memory, network, and disk statistics from the host. You will see inbound traffic and outbound traffic metrics 
along with top processes by CPU, processes by memory, interfaces by incoming and outgoing traffic and number processes.

### Using the Playbook

In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the Filebeat and Metricbeat configuration files to your Ansible container.
- Update the host file to include the ELK server and ELK server IP address. Update the Filebeat and Metricbeat playbook files 
to specify running on the web servers.
- Run the playbook, and navigate to "http://[YOURELKVM];5601/app/kibana" to check that the installation worked as expected.
