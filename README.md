# Projects
## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

[Project Diagram drawio](https://user-images.githubusercontent.com/101853429/159405859-ecf3a22b-98c8-4f8e-a856-4c2f20850c67.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the playbook file may be used to install only certain peices of it, such as filebeat. 

[elk_setup.yml.txt](https://github.com/MartymcShy/Projects/files/8320989/elk_setup.yml.txt)

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly efficient, in addition to protecting access to the network.
- Load balancers can prevent a DoS attack by routing traffic from an overwhelemed machine to a less traffic machine. Placing a gateway router between VMs forces traffic to a single node

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the logs and system CPU usage, memory, file system, disk IO, and network IO statistics

The configuration details of each machine may be found below.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 10.0.0.1   | Linux            |
| Web1     | Web Host | 10.0.0.6   | Linux            |
| Web2     | Web Host | 10.0.0.7   | Linux            |
| Web3     | Web Host | 10.0.0.9   | Linux            |
| ELK      | Web Host | 10.1.0.4   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump Box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- 70.181.172.233

Machines within the network can only be accessed by 52.191.79.19.

A summary of the access policies in place can be found in the table below.

| Name               | Publicly Accessible | Allowed IP Addresses        |
|--------------------|---------------------|-----------------------------|
| SSH-from-Jumpbox   | No                  | 10.0.0.4 10.0.0.6 10.0.09   |
| LetmeIN-SSHjumpbox | Yes                 | 70.181.172.233              |
|  Allow_DVWA        | Yes                 | 70.181.172.233              |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- You can save the ansible playbook and, with just a few modifications, can set up any machine with the same configurations. This makes it very easy to set up multiple machines. 

The playbook implements the following tasks:
- Create a text file called example_playbook.yml
- Edit that text file and include something like
- ---
  name: Configure ELK VM w/ docker
  hosts: elk
  remote_user: [your username]
  become: true
  tasks:
- Now add the tasks that you need in order to download/install/configure/etc.. eg:
- - name: Install docker.io
  apt:
    update_cache: yes
    force_apt_get: yes
    name: docker.io
    state: present

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

[docker_ps_output](https://user-images.githubusercontent.com/101853429/159406013-7b1c294c-689e-4dc0-93af-1eb07bac8ac6.JPG)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- Web1, Web2, and Web3.

We have installed the following Beats on these machines:
- Filebeat and Metricbeat

These Beats allow us to collect the following information from each machine:
- Filebeat collects and monitors log data. 
- Metricbeat monitors the  CPU usage, memory, file system, disk IO, and network IO statistics.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the config file to the ansible folder. 
- Update the hosts file to include the private IP of the ELK machine 
- Run the playbook, and navigate to http://40.70.240.232:5601/app/kibana to check that the installation worked as expected.
