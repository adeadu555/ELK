## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

**Note**: The following image link needs to be updated. Replace `Cloud-Security-Diagram(1).pdf` with the name of your diagram image file.  


These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the install-elk.yml file may be used to install only certain pieces of it, such as Filebeat.

  ---
- name: Config elk server with docker
  hosts: elk
  become: true
  tasks:
   - name: install docker.io
     apt:
       update_cache: yes
       name: docker.io
       state: present
   - name: install python3-pip
     apt:
       name: python3-pip
       state: present
   - name: install docker python module
     pip:
       name: docker
       state: present
   - name: download and launch sebp/elk container
     docker_container:
       name: elk
       image: sebp/elk:761
       state: started
       restart_policy: always
       published_ports:
         - 5601:5601
         - 9200:9200
         - 5044:5044
   - name: use more memory
     sysctl:
        name: vm.max_map_count
        value: "262144"
        state: present
        reload: yes
   - name: enable docker service
     systemd:
       name: docker

This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology
​
The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.
​
Load balancing ensures that the application will be highly protected from DDOS, in addition to restricting overload to the network.
Load balancing protects against Distributed Denial of Service. Jump box is used to manage devices in different security zones.
​
Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the _____ and system _____.
- _TODO: What does Filebeat watch for?_     Log files
- _TODO: What does Metricbeat record?_      metrics from operating systems
​
The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 10.0.0.1   | Linux            |
| TODO     |  Web-1   | 10.1.0.7   | Linux            |
| TODO     |   Web-2  | 10.1.0.8   | Linux            |
| TODO     |          |            |                  |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the __Jumpbox___ machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- _TODO: Add whitelisted IP addresses_

Machines within the network can only be accessed by _____.
- _TODO: Which machine did you allow to access your ELK VM? - The jump-box-provisioner What was its IP address?- 40.112.209.243
​
A summary of the access policies in place can be found in the table below.
​
| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box |  No                 | 10.1.0.4             |
| Web-1    |  No                 | 10.1.0.7             |
| Web-2    |  No                 | 10.1.0.8             |
​
### Elk Configuration
​
Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- _TODO: What is the main advantage of automating configuration with Ansible?_Flexible: You can orchestrate the entire application environment no matter where it's deployed
​
The playbook implements the following tasks:
- _TODO: In 3-5 bullets, explain the steps of the ELK installation play. E.g., install Docker; download image; etc._
- - From your Ansible container, add the new VM to Ansible's hosts file.
	- Create a playbook that installs Docker and configures the container.
	- Run the playbook to launch the container.
- ...
​
The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.
​
ONTAINER ID   IMAGE          COMMAND                  CREATED          STATUS          PORTS                                                                              NAMES
ee64297b15c8   sebp/elk:761   "/usr/local/bin/star…"   20 minutes ago   Up 19 minutes   0.0.0.0:5044->5044/tcp, 0.0.0.0:5601->5601/tcp, 0.0.0.0:9200->9200/tcp, 9300/tcp   elk



![TODO: Update the path with the name of your screenshot of docker ps output](Images/docker_ps_output.png)
​
### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- _TODO: List the IP addresses of the machines you are monitoring_
- Web-1: 10.1.0.7
- Web-2: 10.1.0.8
​
We have installed the following Beats on these machines:
- _TODO: Specify which Beats you successfully installed_
​ 
These Beats allow us to collect the following information from each machine:
- _TODO: In 1-2 sentences, explain what kind of data each beat collects, and provide 1 example of what you expect to see. E.g., `Winlogbeat` collects Windows logs, which we use to track user logon events, etc._
​
### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 
​
SSH into the control node and follow the steps below:
- Copy the _____ file to _____.
- Update the _____ file to include...
- Run the playbook, and navigate to ____ to check that the installation worked as expected.
​
_TODO: Answer the following questions to fill in the blanks:_
- _Which file is the playbook? Where do you copy it?_
- _Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?_
- _Which URL do you navigate to in order to check that the ELK server is running?
​
_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._
