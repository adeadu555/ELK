Part 1 - ## Automated ELK Stack Deployment





Part 2 - ## ELK-Project





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

Only the Jumpbox machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- _TODO: Add whitelisted IP addresses_

Machines within the network can only be accessed by _____.
-  Which machine did you allow to access your ELK VM? - The jump-box-provisioner 
- What was its IP address?- 40.112.209.243
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

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
What is the main advantage of automating configuration with Ansible?
Flexibility: You can orchestrate the entire application environment no matter where it's deployed

The playbook implements the following tasks:
 In 3-5 bullets, explain the steps of the ELK installation play. E.g., install Docker; download image; etc._
- From your Ansible container, add the new VM to Ansible's hosts file.
- Create a playbook that installs Docker and configures the container.
- Run the playbook to launch the container.

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

ONTAINER ID   IMAGE          COMMAND                  CREATED          STATUS          PORTS                                                                              NAMES
ee64297b15c8   sebp/elk:761   "/usr/local/bin/star…"   20 minutes ago   Up 19 minutes   0.0.0.0:5044->5044/tcp, 0.0.0.0:5601->5601/tcp, 0.0.0.0:9200->9200/tcp, 9300/tcp   elk



### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- _TODO: List the IP addresses of the machines you are monitoring_
- Web-1: 10.1.0.7
- Web-2: 10.1.0.8
​
We have installed the following Beats on these machines:
: Specify which Beats you successfully installed_
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
- Run the playbook, and navigate to _filebeat installation page on the ELK server GUI___ to check that the installation worked as expected.



_TODO: Answer the following questions to fill in the blanks:_
- _Which file is the playbook? Where do you copy it?_
- _Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?_
- _Which URL do you navigate to in order to check that the ELK server is running?
​
_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._



# ELK
ELK-Project

Prerequisites for the ELK project:


User must have installed and configured:
A Resource Group: Red-Team
A network Security Group - RedTeam-Firewall
Virtual Machine - Jump-Box-Provisioner
virtual machines - Web-1 and Web-2.

1.Activities for Azure setup and ELK Server configuration

A. Create a Resource Group on Azure
B. Create a new Virtual Network - ELK-NET
C. Create peer connection between your virtual Networks
D. Create New Virtual Machine
E. Configure new Virtual Machine using Ansible
F. Add ELK to Ansible's hosts file
G. Create playbook to configure ELK server
H. SSH into ELK server
I. Restrict access to ELK virtual Machine using Azure's Network Security Group (NSG)

2.Activities for Filebeat configuration

A. Install filebeat on the DWVA Container
B. Create Filebeat configuration file
C. Create Filebeat Installation play
D. Verify installation and playbook




2. Description of Deployment

A. Creation of Red-Team Resource Group on Azure
    Instructions to follow - Creating a resource Group
    Go to the top bar ---> [Type] Resource Group 
    [Click] + create
    Go To Basics Tab
    Enter "US West US" under Reqion
    Enter Resource Group Name: Red-Team
    [Click Review & Create]
    [Create]

B. Add a Virtual Network ELK-NET in a new Region from the Red-Team Resource group
Next step is to add Virtual Network (a collection of virtual machines that can communicate with one another)

    Type -- Virtual network on Top bar

    Select your resource Group
    Enter your virtual network - ELK-NET
    Click Next: IP addresses
    Default: 10.1.0.0/16

    Go to Security Tab Next: leave the defaults as well

    Go to Tag Tab: Leave as it is

    Go to Review & Create 

    Running final validation ..... Validation passed

    Then click on Create [Create]

    ....Initializing Deployment to 
    ....Your deployment is complete
    
    
    Image: Image1-VirtualNetwork-ELK-NET
    
C.  Create peer connection to allow traffic pass between virtual networks and regions

	Navigate to 'Virtual Network' in the Azure Portal.
	Select your new vNet to view it's details.
	Under 'Settings' on the left side, select 'Peerings'.
	Click the + Add button to create a new Peering.
    
    Image: Image2-Elk-Peering
    
    
 D. Create new Virtual Machine - ELK Server
 
 Image: Image3 - ELK-Server
 
 E. From Ansible container, configure the newly created virtual machine
 
 F. Add ELK to Ansible's hosts file
 
 
 G. Playbook that installs Docker
 
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
 
 
 H. SSH to ELK server
 
 root@7a83e6be604d:~# ssh azadmin@20.97.26.76
The authenticity of host '20.97.26.76 (20.97.26.76)' can't be established.
ECDSA key fingerprint is SHA256:MsKmwnMfem6AtnTHn696NbCgFo9MVXBQuL9qsph/xeo.
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added '20.97.26.76' (ECDSA) to the list of known hosts.
Welcome to Ubuntu 18.04.5 LTS (GNU/Linux 5.4.0-1046-azure x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

  System information as of Mon Apr 26 17:46:26 UTC 2021

  System load:  0.0               Processes:           118
  Usage of /:   4.5% of 28.90GB   Users logged in:     0
  Memory usage: 5%                IP address for eth0: 10.1.0.4
  Swap usage:   0%

0 packages can be updated.
0 of these updates are security updates.



The programs included with the Ubuntu system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Ubuntu comes with ABSOLUTELY NO WARRANTY, to the extent permitted by
applicable law.

azadmin@ELK-SERVER:~$


To start ELK.......

azadmin@ELK-SERVER:~$ sudo docker container list -a
CONTAINER ID   IMAGE          COMMAND                  CREATED          STATUS          PORTS                                                                              NAMES
ee64297b15c8   sebp/elk:761   "/usr/local/bin/star…"   11 minutes ago   Up 11 minutes   0.0.0.0:5044->5044/tcp, 0.0.0.0:5601->5601/tcp, 0.0.0.0:9200->9200/tcp, 9300/tcp   elk
azadmin@ELK-SERVER:~$ sudo docker start elk
elk
azadmin@ELK-SERVER:~$ sudo docker ps
CONTAINER ID   IMAGE          COMMAND                  CREATED          STATUS          PORTS                                                                              NAMES
ee64297b15c8   sebp/elk:761   "/usr/local/bin/star…"   20 minutes ago   Up 19 minutes   0.0.0.0:5044->5044/tcp, 0.0.0.0:5601->5601/tcp, 0.0.0.0:9200->9200/tcp, 9300/tcp   elk



Kibana.......

azadmin@ELK-SERVER:~$ curl localhost:5601/app/kibana
<!DOCTYPE html><html lang="en"><head><meta charSet="utf-8"/><meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1"/><meta name="viewport" content="width=device-width"/><title>Kibana</title><style>
        
        @font-face {
          font-family: 'Inter UI';
          font-style: normal;
          font-weight: 100;
          src: url('/ui/fonts/inter_ui/Inter-UI-Thin-BETA.woff2') format('woff2'), url('/ui/fonts/inter_ui/Inter-UI-Thin-BETA.woff') format('woff');
        }

        @font-face {
          font-family: 'Inter UI';
          font-style: italic;
          font-weight: 100;
          src: url('/ui/fonts/inter_ui/Inter-UI-ThinItalic-BETA.woff2') format('woff2'), url('/ui/fonts/inter_ui/Inter-UI-ThinItalic-BETA.woff') format('woff');
        }

        @font-face {
          font-family: 'Inter UI';
          font-style: normal;
          font-weight: 200;
          src: url('/ui/fonts/inter_ui/Inter-UI-ExtraLight-BETA.woff2') format('woff2'), url('/ui/fonts/inter_ui/Inter-UI-ExtraLight-BETA.woff') format('woff');
        }

        @font-face {
          font-family: 'Inter UI';
          font-style: italic;
          font-weight: 200;
          src: url('/ui/fonts/inter_ui/Inter-UI-ExtraLightItalic-BETA.woff2') format('woff2'), url('/ui/fonts/inter_ui/Inter-UI-ExtraLightItalic-BETA.woff') format('woff');
        }

        @font-face {
          font-family: 'Inter UI';
          font-style: normal;
          font-weight: 300;
          src: url('/ui/fonts/inter_ui/Inter-UI-Light-BETA.woff2') format('woff2'), url('/ui/fonts/inter_ui/Inter-UI-Light-BETA.woff') format('woff');
        }

        @font-face {
          font-family: 'Inter UI';
          font-style: italic;
          font-weight: 300;
          src: url('/ui/fonts/inter_ui/Inter-UI-LightItalic-BETA.woff2') format('woff2'), url('/ui/fonts/inter_ui/Inter-UI-LightItalic-BETA.woff') format('woff');
        }

        @font-face {
          font-family: 'Inter UI';
          font-style: normal;
          font-weight: 400;
          src: url('/ui/fonts/inter_ui/Inter-UI-Regular.woff2') format('woff2'), url('/ui/fonts/inter_ui/Inter-UI-Regular.woff') format('woff');
        }

        @font-face {
          font-family: 'Inter UI';
          font-style: italic;
          font-weight: 400;
          src: url('/ui/fonts/inter_ui/Inter-UI-Italic.woff2') format('woff2'), url('/ui/fonts/inter_ui/Inter-UI-Italic.woff') format('woff');
        }

        @font-face {
          font-family: 'Inter UI';
          font-style: normal;
          font-weight: 500;
          src: url('/ui/fonts/inter_ui/Inter-UI-Medium.woff2') format('woff2'), url('/ui/fonts/inter_ui/Inter-UI-Medium.woff') format('woff');
        }

        @font-face {
          font-family: 'Inter UI';
          font-style: italic;
          font-weight: 500;
          src: url('/ui/fonts/inter_ui/Inter-UI-MediumItalic.woff2') format('woff2'), url('/ui/fonts/inter_ui/Inter-UI-MediumItalic.woff') format('woff');
        }

        @font-face {
          font-family: 'Inter UI';
          font-style: normal;
          font-weight: 600;
          src: url('/ui/fonts/inter_ui/Inter-UI-SemiBold.woff2') format('woff2'), url('/ui/fonts/inter_ui/Inter-UI-SemiBold.woff') format('woff');
        }

        @font-face {
          font-family: 'Inter UI';
          font-style: italic;
          font-weight: 600;
          src: url('/ui/fonts/inter_ui/Inter-UI-SemiBoldItalic.woff2') format('woff2'), url('/ui/fonts/inter_ui/Inter-UI-SemiBoldItalic.woff') format('woff');
        }

        @font-face {
          font-family: 'Inter UI';
          font-style: normal;
          font-weight: 700;
          src: url('/ui/fonts/inter_ui/Inter-UI-Bold.woff2') format('woff2'), url('/ui/fonts/inter_ui/Inter-UI-Bold.woff') format('woff');
        }

        @font-face {
          font-family: 'Inter UI';
          font-style: italic;
          font-weight: 700;
          src: url('/ui/fonts/inter_ui/Inter-UI-BoldItalic.woff2') format('woff2'), url('/ui/fonts/inter_ui/Inter-UI-BoldItalic.woff') format('woff');
        }

        @font-face {
          font-family: 'Inter UI';
          font-style: normal;
          font-weight: 800;
          src: url('/ui/fonts/inter_ui/Inter-UI-ExtraBold.woff2') format('woff2'), url('/ui/fonts/inter_ui/Inter-UI-ExtraBold.woff') format('woff');
        }

        @font-face {
          font-family: 'Inter UI';
          font-style: italic;
          font-weight: 800;
          src: url('/ui/fonts/inter_ui/Inter-UI-ExtraBoldItalic.woff2') format('woff2'), url('/ui/fonts/inter_ui/Inter-UI-ExtraBoldItalic.woff') format('woff');
        }

        @font-face {
          font-family: 'Inter UI';
          font-style: normal;
          font-weight: 900;
          src: url('/ui/fonts/inter_ui/Inter-UI-Black.woff2') format('woff2'), url('/ui/fonts/inter_ui/Inter-UI-Black.woff') format('woff');
        }

        @font-face {
          font-family: 'Inter UI';
          font-style: italic;
          font-weight: 900;
          src: url('/ui/fonts/inter_ui/Inter-UI-BlackItalic.woff2') format('woff2'), url('/ui/fonts/inter_ui/Inter-UI-BlackItalic.woff') format('woff');
        }

        @font-face {
          font-family: 'Roboto Mono';
          font-style: normal;
          font-weight: 400;
          src: local('Roboto Mono'), local('RobotoMono-Regular'), url('/ui/fonts/roboto_mono/RobotoMono-Regular.ttf') format('woff2');
          unicode-range: U+0000-00FF, U+0131, U+0152-0153, U+02BB-02BC, U+02C6, U+02DA, U+02DC, U+2000-206F, U+2074, U+20AC, U+2122, U+2191, U+2193, U+2212, U+2215, U+FEFF, U+FFFD;
        }

        @font-face {
          font-family: 'Roboto Mono';
          font-style: italic;
          font-weight: 400;
          src: local('Roboto Mono Italic'), local('RobotoMono-Italic'), url('/ui/fonts/roboto_mono/RobotoMono-Italic.ttf') format('ttf');
          unicode-range: U+0000-00FF, U+0131, U+0152-0153, U+02BB-02BC, U+02C6, U+02DA, U+02DC, U+2000-206F, U+2074, U+20AC, U+2122, U+2191, U+2193, U+2212, U+2215, U+FEFF, U+FFFD;
        }

        @font-face {
          font-family: 'Roboto Mono';
          font-style: normal;
          font-weight: 700;
          src: local('Roboto Mono Bold'), local('RobotoMono-Bold'), url('/ui/fonts/roboto_mono/RobotoMono-Bold.ttf') format('woff2');
          unicode-range: U+0000-00FF, U+0131, U+0152-0153, U+02BB-02BC, U+02C6, U+02DA, U+02DC, U+2000-206F, U+2074, U+20AC, U+2122, U+2191, U+2193, U+2212, U+2215, U+FEFF, U+FFFD;
        }

        @font-face {
          font-family: 'Roboto Mono';
          font-style: italic;
          font-weight: 700;
          src: local('Roboto Mono Bold Italic'), local('RobotoMono-BoldItalic'), url('/ui/fonts/roboto_mono/RobotoMono-BoldItalic.ttf') format('woff2');
          unicode-range: U+0000-00FF, U+0131, U+0152-0153, U+02BB-02BC, U+02C6, U+02DA, U+02DC, U+2000-206F, U+2074, U+20AC, U+2122, U+2191, U+2193, U+2212, U+2215, U+FEFF, U+FFFD;
        }
        /*
        Single variable font.

        Note that you may want to do something like this to make sure you're serving
        constant fonts to older browsers:
        html {
          font-family: 'Inter UI', sans-serif;
        }
        @supports (font-variation-settings: normal) {
          html {
            font-family: 'Inter UI var', sans-serif;
          }
        }

        BUGS:
        - Safari 12.0 will default to italic instead of regular when font-weight
          is provided in a @font-face declaration.
          Workaround: Use 'Inter UI var alt' for Safari, or explicitly set
          `font-variation-settings: 'slnt' DEGREE`.

        @font-face {
          font-family: 'Inter UI var';
          font-weight: 100 900;
          font-style: oblique 0deg 10deg;
          src:
            url('/ui/fonts/inter_ui/Inter-UI.var.woff2') format('woff2-variations'),
            url('/ui/fonts/inter_ui/Inter-UI.var.woff2') format('woff2');
        }

        'Inter UI var alt' is recommended for Safari and Edge, for reliable italics.

        @supports (font-variation-settings: normal) {
          html {
            font-family: 'Inter UI var alt', sans-serif;
          }
        }

        @font-face {
          font-family: 'Inter UI var alt';
          font-weight: 100 900;
          font-style: normal;
          font-named-instance: 'Regular';
          src:
            url('/ui/fonts/inter_ui/Inter-UI-upright.var.woff2') format('woff2 supports variations(gvar)'),
            url('/ui/fonts/inter_ui/Inter-UI-upright.var.woff2') format('woff2-variations'),
            url('/ui/fonts/inter_ui/Inter-UI-upright.var.woff2') format('woff2');
        }
        @font-face {
          font-family: 'Inter UI var alt';
          font-weight: 100 900;
          font-style: italic;
          font-named-instance: 'Italic';
          src:
            url('/ui/fonts/inter_ui/Inter-UI-italic.var.woff2') format('woff2 supports variations(gvar)'),
            url('/ui/fonts/inter_ui/Inter-UI-italic.var.woff2') format('woff2-variations'),
            url('/ui/fonts/inter_ui/Inter-UI-italic.var.woff2') format('woff2');
        }
        */
      </style><link rel="apple-touch-icon" sizes="180x180" href="/ui/favicons/apple-touch-icon.png"/><link rel="icon" type="image/png" sizes="32x32" href="/ui/favicons/favicon-32x32.png"/><link rel="icon" type="image/png" sizes="16x16" href="/ui/favicons/favicon-16x16.png"/><link rel="manifest" href="/ui/favicons/manifest.json"/><link rel="mask-icon" color="#e8488b" href="/ui/favicons/safari-pinned-tab.svg"/><link rel="shortcut icon" href="/ui/favicons/favicon.ico"/><meta name="msapplication-config" content="/ui/favicons/browserconfig.xml"/><meta name="theme-color" content="#ffffff"/><style>
          * {
            box-sizing: border-box;
          }

          body, html {
            width: 100%;
            height: 100%;
            margin: 0;
          }

          .kibanaWelcomeView {
            height: 100%;
            display: -webkit-box;
            display: -webkit-flex;
            display: -ms-flexbox;
            display: flex;
            -webkit-box-flex: 1;
            -webkit-flex: 1 0 auto;
                -ms-flex: 1 0 auto;
                    flex: 1 0 auto;
            -webkit-box-orient: vertical;
            -webkit-box-direction: normal;
            -webkit-flex-direction: column;
                -ms-flex-direction: column;
                    flex-direction: column;
            -webkit-box-align: center;
            -webkit-align-items: center;
                -ms-flex-align: center;
                    align-items: center;
            -webkit-box-pack: center;
            -webkit-justify-content: center;
                -ms-flex-pack: center;
                    justify-content: center;
          }

          .kibanaWelcomeLogo {
            width: 60px;
            height: 60px;
            margin: 10px 0 10px 20px;
            background-repeat: no-repeat;
            background-size: contain;
            /* SVG optimized according to http://codepen.io/tigt/post/optimizing-svgs-in-data-uris */
            background-image: url('data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIzMCIgaGVpZ2h0PSIzOSIgdmlld0JveD0iMCAwIDMwIDM5Ij4gIDxnIGZpbGw9Im5vbmUiIGZpbGwtcnVsZT0iZXZlbm9kZCI+ICAgIDxwb2x5Z29uIGZpbGw9IiNGMDRFOTgiIHBvaW50cz0iMCAwIDAgMzQuNTQ3IDI5LjkyMiAuMDIiLz4gICAgPHBhdGggZmlsbD0iIzM0Mzc0MSIgZD0iTTAsMTQuNCBMMCwzNC41NDY4IEwxNC4yODcyLDE4LjA2MTIgQzEwLjA0MTYsMTUuNzM4IDUuMTgwNCwxNC40IDAsMTQuNCIvPiAgICA8cGF0aCBmaWxsPSIjMDBCRkIzIiBkPSJNMTcuMzc0MiwxOS45OTY4IEwyLjcyMSwzNi45MDQ4IEwxLjQzMzQsMzguMzg5MiBMMjkuMjYzOCwzOC4zODkyIEMyNy43NjE0LDMwLjgzODggMjMuNDA0MiwyNC4zMjY0IDE3LjM3NDIsMTkuOTk2OCIvPiAgPC9nPjwvc3ZnPg==');
          }

          .kibanaWelcomeTitle {
            color: #000;
            font-size: 20px;
            font-family: sans-serif;
            margin-top: 20px;
            animation: fadeIn 1s ease-in-out;
            animation-fill-mode: forwards;
            opacity: 0;
            animation-delay: 1.0s;
          }

          .kibanaWelcomeText {
            font-size: 14px;
            font-family: sans-serif;
            color: #98a2b3;
            animation: fadeIn 1s ease-in-out;
            animation-fill-mode: forwards;
            opacity: 0;
            animation-delay: 1.0s;
          }

          .kibanaLoaderWrap {
            height: 128px;
            width: 128px;
            position: relative;
            margin-top: 40px;
          }

          .kibanaLoaderWrap + * {
            margin-top: 24px;
          }

          .kibanaLoader {
            height: 128px;
            width: 128px;
            margin: 0 auto;
            position: relative;
            border: 2px solid transparent;
            border-top: 2px solid #017d73;
            border-radius: 100%;
            display: block;
            opacity: 0;
            animation: rotation .75s .5s infinite linear, fadeIn 1s .5s ease-in-out forwards;
          }

          .kibanaWelcomeLogoCircle {
            position: absolute;
            left: 4px;
            top: 4px;
            width: 120px;
            height: 120px;
            padding: 20px;
            background-color: #fff;
            border-radius: 50%;
            animation: bounceIn .5s ease-in-out;
          }

          @keyframes rotation {
            from {
              transform: rotate(0deg);
            }
            to {
              transform: rotate(359deg);
            }
          }
          @keyframes fadeIn {
            from {
              opacity: 0;
            }
            to {
              opacity: 1;
            }
          }
          @keyframes bounceIn {
            0% {
              opacity: 0;
              transform: scale(.1);
            }
            80% {
              opacity: .5;
              transform: scale(1.2);
            }
            100% {
              opacity: 1;
              transform: scale(1);
            }
          }
        </style></head><body><kbn-csp data="{&quot;strictCsp&quot;:false}"></kbn-csp><kbn-injected-metadata data="{&quot;version&quot;:&quot;7.6.1&quot;,&quot;buildNumber&quot;:29118,&quot;branch&quot;:&quot;7.6&quot;,&quot;basePath&quot;:&quot;&quot;,&quot;env&quot;:{&quot;homeDir&quot;:&quot;/opt/kibana&quot;,&quot;configDir&quot;:&quot;/opt/kibana/config&quot;,&quot;binDir&quot;:&quot;/opt/kibana/bin&quot;,&quot;logDir&quot;:&quot;/opt/kibana/log&quot;,&quot;pluginSearchPaths&quot;:[&quot;/opt/kibana/src/plugins&quot;,&quot;/opt/kibana/x-pack/plugins&quot;,&quot;/opt/kibana/plugins&quot;,&quot;/opt/kibana-extra&quot;],&quot;packageInfo&quot;:{&quot;branch&quot;:&quot;7.6&quot;,&quot;buildNum&quot;:29118,&quot;buildSha&quot;:&quot;5ddabf8510131ebf173762b7405e5e18f2757c12&quot;,&quot;version&quot;:&quot;7.6.1&quot;,&quot;dist&quot;:true},&quot;mode&quot;:{&quot;dev&quot;:false,&quot;name&quot;:&quot;production&quot;,&quot;prod&quot;:true},&quot;cliArgs&quot;:{&quot;dev&quot;:false,&quot;open&quot;:false,&quot;quiet&quot;:false,&quot;silent&quot;:false,&quot;watch&quot;:false,&quot;repl&quot;:false,&quot;runExamples&quot;:false,&quot;basePath&quot;:false,&quot;optimize&quot;:false,&quot;oss&quot;:false},&quot;configs&quot;:[&quot;/opt/kibana/config/kibana.yml&quot;],&quot;isDevClusterMaster&quot;:false},&quot;legacyMode&quot;:true,&quot;i18n&quot;:{&quot;translationsUrl&quot;:&quot;/translations/en.json&quot;},&quot;csp&quot;:{&quot;warnLegacyBrowsers&quot;:true},&quot;vars&quot;:{&quot;activeSpace&quot;:{&quot;valid&quot;:true,&quot;space&quot;:{&quot;id&quot;:&quot;default&quot;,&quot;name&quot;:&quot;Default&quot;,&quot;description&quot;:&quot;This is your default space!&quot;,&quot;color&quot;:&quot;#00bfb3&quot;,&quot;disabledFeatures&quot;:[],&quot;_reserved&quot;:true}},&quot;spacesEnabled&quot;:true,&quot;monitoringUiEnabled&quot;:true,&quot;serverBasePath&quot;:&quot;&quot;,&quot;secureCookies&quot;:false,&quot;session&quot;:{&quot;tenant&quot;:&quot;&quot;},&quot;enableSpaceAwarePrivileges&quot;:true,&quot;logoutUrl&quot;:&quot;/logout&quot;,&quot;mlEnabled&quot;:true,&quot;apmUiEnabled&quot;:true,&quot;apmIndexPatternTitle&quot;:&quot;apm-*&quot;,&quot;apmServiceMapEnabled&quot;:false,&quot;showMapVisualizationTypes&quot;:false,&quot;showMapsInspectorAdapter&quot;:false,&quot;preserveDrawingBuffer&quot;:false,&quot;isEmsEnabled&quot;:true,&quot;emsFontLibraryUrl&quot;:&quot;https://tiles.maps.elastic.co/fonts/{fontstack}/{range}.pbf&quot;,&quot;emsTileLayerId&quot;:{&quot;bright&quot;:&quot;road_map&quot;,&quot;desaturated&quot;:&quot;road_map_desaturated&quot;,&quot;dark&quot;:&quot;dark_map&quot;},&quot;proxyElasticMapsServiceInMaps&quot;:false,&quot;emsFileApiUrl&quot;:&quot;https://vector.maps.elastic.co&quot;,&quot;emsTileApiUrl&quot;:&quot;https://tiles.maps.elastic.co&quot;,&quot;emsLandingPageUrl&quot;:&quot;https://maps.elastic.co/v7.6&quot;,&quot;kbnPkgVersion&quot;:&quot;7.6.1&quot;,&quot;regionmapLayers&quot;:[],&quot;tilemap&quot;:{&quot;options&quot;:{&quot;default&quot;:true,&quot;minZoom&quot;:0,&quot;maxZoom&quot;:10}},&quot;licenseManagementUiEnabled&quot;:true,&quot;ilmUiEnabled&quot;:true,&quot;remoteClustersUiEnabled&quot;:true,&quot;ccrUiEnabled&quot;:true,&quot;slmUiEnabled&quot;:true,&quot;elasticsearchUrl&quot;:&quot;http://localhost:9200/&quot;,&quot;esRequestTimeout&quot;:30000,&quot;esShardTimeout&quot;:30000,&quot;esApiVersion&quot;:&quot;7.x&quot;,&quot;kbnIndex&quot;:&quot;.kibana&quot;,&quot;kbnBaseUrl&quot;:&quot;/app/kibana&quot;,&quot;mapConfig&quot;:{&quot;includeElasticMapsService&quot;:true,&quot;proxyElasticMapsServiceInMaps&quot;:false,&quot;tilemap&quot;:{&quot;options&quot;:{&quot;default&quot;:true,&quot;minZoom&quot;:0,&quot;maxZoom&quot;:10}},&quot;regionmap&quot;:{&quot;includeElasticMapsService&quot;:true,&quot;layers&quot;:[]},&quot;manifestServiceUrl&quot;:&quot;&quot;,&quot;emsFileApiUrl&quot;:&quot;https://vector.maps.elastic.co&quot;,&quot;emsTileApiUrl&quot;:&quot;https://tiles.maps.elastic.co&quot;,&quot;emsLandingPageUrl&quot;:&quot;https://maps.elastic.co/v7.6&quot;,&quot;emsFontLibraryUrl&quot;:&quot;https://tiles.maps.elastic.co/fonts/{fontstack}/{range}.pbf&quot;,&quot;emsTileLayerId&quot;:{&quot;bright&quot;:&quot;road_map&quot;,&quot;desaturated&quot;:&quot;road_map_desaturated&quot;,&quot;dark&quot;:&quot;dark_map&quot;}},&quot;tilemapsConfig&quot;:{&quot;deprecated&quot;:{&quot;isOverridden&quot;:false,&quot;config&quot;:{&quot;options&quot;:{&quot;default&quot;:true,&quot;minZoom&quot;:0,&quot;maxZoom&quot;:10}}}},&quot;newsfeed&quot;:{&quot;service&quot;:{&quot;pathTemplate&quot;:&quot;/kibana/v{VERSION}.json&quot;,&quot;urlRoot&quot;:&quot;https://feeds.elastic.co&quot;},&quot;defaultLanguage&quot;:&quot;en&quot;,&quot;mainInterval&quot;:120000,&quot;fetchInterval&quot;:86400000},&quot;regionmap&quot;:{&quot;includeElasticMapsService&quot;:true,&quot;layers&quot;:[]},&quot;isStatusPageAnonymous&quot;:false,&quot;telemetryEnabled&quot;:true,&quot;telemetryUrl&quot;:&quot;https://telemetry.elastic.co/xpack/v2/send&quot;,&quot;telemetryBanner&quot;:true,&quot;telemetryOptedIn&quot;:true,&quot;telemetryOptInStatusUrl&quot;:&quot;https://telemetry.elastic.co/opt_in_status/v2/send&quot;,&quot;allowChangingOptInStatus&quot;:true,&quot;telemetrySendUsageFrom&quot;:&quot;browser&quot;,&quot;telemetryNotifyUserAboutOptInDefault&quot;:true,&quot;timelionUiEnabled&quot;:false,&quot;enableExternalUrls&quot;:false,&quot;reportingPollConfig&quot;:{&quot;jobCompletionNotifier&quot;:{&quot;interval&quot;:10000,&quot;intervalErrorMultiplier&quot;:5},&quot;jobsRefresh&quot;:{&quot;interval&quot;:5000,&quot;intervalErrorMultiplier&quot;:5}},&quot;enablePanelActionDownload&quot;:true,&quot;kbnDefaultAppId&quot;:&quot;home&quot;,&quot;disableWelcomeScreen&quot;:false,&quot;importAndExportableTypes&quot;:[&quot;config&quot;,&quot;map&quot;,&quot;canvas-workpad&quot;,&quot;canvas-element&quot;,&quot;lens&quot;,&quot;query&quot;,&quot;index-pattern&quot;,&quot;visualization&quot;,&quot;search&quot;,&quot;dashboard&quot;,&quot;url&quot;],&quot;autocompleteTerminateAfter&quot;:100000,&quot;autocompleteTimeout&quot;:1000,&quot;xpackInitialInfo&quot;:{&quot;license&quot;:{&quot;type&quot;:&quot;basic&quot;,&quot;isActive&quot;:true},&quot;features&quot;:{&quot;security&quot;:{&quot;showLogin&quot;:false,&quot;allowLogin&quot;:false,&quot;showLinks&quot;:false,&quot;showRoleMappingsManagement&quot;:false,&quot;allowRoleDocumentLevelSecurity&quot;:false,&quot;allowRoleFieldLevelSecurity&quot;:false,&quot;allowRbac&quot;:false,&quot;linksMessage&quot;:&quot;Access is denied because Security is disabled in Elasticsearch.&quot;},&quot;searchprofiler&quot;:{&quot;showAppLink&quot;:true,&quot;enableAppLink&quot;:true},&quot;ml&quot;:{&quot;isAvailable&quot;:true,&quot;showLinks&quot;:true,&quot;enableLinks&quot;:true,&quot;licenseType&quot;:0,&quot;hasExpired&quot;:false},&quot;tilemap&quot;:{&quot;license&quot;:{&quot;uid&quot;:&quot;37aefe84-13f2-43bd-8a40-45480ddda989&quot;,&quot;active&quot;:true,&quot;valid&quot;:true}},&quot;watcher&quot;:{&quot;status&quot;:&quot;INVALID&quot;,&quot;message&quot;:&quot;Your basic license does not support Watcher. Please upgrade your license.&quot;},&quot;grokdebugger&quot;:{&quot;enableLink&quot;:true,&quot;enableAPIRoute&quot;:true},&quot;logstash&quot;:{&quot;isAvailable&quot;:false,&quot;enableLinks&quot;:false,&quot;isReadOnly&quot;:false,&quot;message&quot;:&quot;Security must be enabled in order to use Logstash pipeline management features. Please set xpack.security.enabled: true in your elasticsearch.yml.&quot;},&quot;beatsManagement&quot;:{&quot;security&quot;:{&quot;enabled&quot;:false,&quot;available&quot;:true},&quot;settings&quot;:{&quot;enabled&quot;:true,&quot;defaultUserRoles&quot;:[&quot;superuser&quot;],&quot;encryptionKey&quot;:&quot;xpack_beats_default_encryptionKey&quot;,&quot;enrollmentTokensTtlInSeconds&quot;:600}},&quot;index_management&quot;:{&quot;status&quot;:&quot;VALID&quot;},&quot;index_lifecycle_management&quot;:{&quot;isAvailable&quot;:true,&quot;showLinks&quot;:true,&quot;enableLinks&quot;:true},&quot;rollup&quot;:{&quot;isAvailable&quot;:true,&quot;showLinks&quot;:true,&quot;enableLinks&quot;:true},&quot;transform&quot;:{&quot;status&quot;:&quot;VALID&quot;},&quot;remote_clusters&quot;:{&quot;status&quot;:&quot;VALID&quot;},&quot;cross_cluster_replication&quot;:{&quot;isAvailable&quot;:false,&quot;isActive&quot;:false,&quot;message&quot;:&quot;Your basic license does not support Cross-Cluster Replication. Please upgrade your license.&quot;},&quot;snapshot_restore&quot;:{&quot;status&quot;:&quot;VALID&quot;},&quot;monitoring&quot;:{&quot;clusterAlerts&quot;:{&quot;enabled&quot;:false},&quot;message&quot;:&quot;Cluster Alerts are not displayed if Watcher is disabled or the [monitoring] cluster&#x27;s current license is Basic.&quot;},&quot;reporting&quot;:{&quot;csv&quot;:{&quot;showLinks&quot;:true,&quot;enableLinks&quot;:true},&quot;csv_from_savedobject&quot;:{&quot;showLinks&quot;:true,&quot;enableLinks&quot;:true},&quot;png&quot;:{&quot;showLinks&quot;:false,&quot;enableLinks&quot;:false,&quot;message&quot;:&quot;Your basic license does not support PNG Reporting. Please upgrade your license.&quot;},&quot;printablePdf&quot;:{&quot;showLinks&quot;:false,&quot;enableLinks&quot;:false,&quot;message&quot;:&quot;Your basic license does not support PDF Reporting. Please upgrade your license.&quot;},&quot;management&quot;:{&quot;showLinks&quot;:true,&quot;enableLinks&quot;:true,&quot;jobTypes&quot;:[&quot;csv&quot;,&quot;csv_from_savedobject&quot;]}}}}},&quot;uiPlugins&quot;:[{&quot;id&quot;:&quot;licensing&quot;,&quot;plugin&quot;:{&quot;id&quot;:&quot;licensing&quot;,&quot;configPath&quot;:[&quot;xpack&quot;,&quot;licensing&quot;],&quot;requiredPlugins&quot;:[],&quot;optionalPlugins&quot;:[]},&quot;config&quot;:{}},{&quot;id&quot;:&quot;usageCollection&quot;,&quot;plugin&quot;:{&quot;id&quot;:&quot;usageCollection&quot;,&quot;configPath&quot;:[&quot;usageCollection&quot;],&quot;requiredPlugins&quot;:[],&quot;optionalPlugins&quot;:[]},&quot;config&quot;:{&quot;uiMetric&quot;:{&quot;enabled&quot;:true,&quot;debug&quot;:false}}},{&quot;id&quot;:&quot;security&quot;,&quot;plugin&quot;:{&quot;id&quot;:&quot;security&quot;,&quot;configPath&quot;:[&quot;xpack&quot;,&quot;security&quot;],&quot;requiredPlugins&quot;:[&quot;licensing&quot;],&quot;optionalPlugins&quot;:[]},&quot;config&quot;:{}},{&quot;id&quot;:&quot;reporting&quot;,&quot;plugin&quot;:{&quot;id&quot;:&quot;reporting&quot;,&quot;configPath&quot;:&quot;reporting&quot;,&quot;requiredPlugins&quot;:[],&quot;optionalPlugins&quot;:[]},&quot;config&quot;:{}},{&quot;id&quot;:&quot;uiActions&quot;,&quot;plugin&quot;:{&quot;id&quot;:&quot;uiActions&quot;,&quot;configPath&quot;:&quot;uiActions&quot;,&quot;requiredPlugins&quot;:[],&quot;optionalPlugins&quot;:[]},&quot;config&quot;:{}},{&quot;id&quot;:&quot;data&quot;,&quot;plugin&quot;:{&quot;id&quot;:&quot;data&quot;,&quot;configPath&quot;:&quot;data&quot;,&quot;requiredPlugins&quot;:[&quot;uiActions&quot;],&quot;optionalPlugins&quot;:[&quot;usageCollection&quot;]},&quot;config&quot;:{}},{&quot;id&quot;:&quot;navigation&quot;,&quot;plugin&quot;:{&quot;id&quot;:&quot;navigation&quot;,&quot;configPath&quot;:&quot;navigation&quot;,&quot;requiredPlugins&quot;:[&quot;data&quot;],&quot;optionalPlugins&quot;:[]},&quot;config&quot;:{}},{&quot;id&quot;:&quot;status_page&quot;,&quot;plugin&quot;:{&quot;id&quot;:&quot;status_page&quot;,&quot;configPath&quot;:&quot;status_page&quot;,&quot;requiredPlugins&quot;:[],&quot;optionalPlugins&quot;:[]},&quot;config&quot;:{}},{&quot;id&quot;:&quot;share&quot;,&quot;plugin&quot;:{&quot;id&quot;:&quot;share&quot;,&quot;configPath&quot;:&quot;share&quot;,&quot;requiredPlugins&quot;:[],&quot;optionalPlugins&quot;:[]},&quot;config&quot;:{}},{&quot;id&quot;:&quot;newsfeed&quot;,&quot;plugin&quot;:{&quot;id&quot;:&quot;newsfeed&quot;,&quot;configPath&quot;:&quot;newsfeed&quot;,&quot;requiredPlugins&quot;:[],&quot;optionalPlugins&quot;:[]},&quot;config&quot;:{}},{&quot;id&quot;:&quot;kibana_legacy&quot;,&quot;plugin&quot;:{&quot;id&quot;:&quot;kibana_legacy&quot;,&quot;configPath&quot;:&quot;kibana_legacy&quot;,&quot;requiredPlugins&quot;:[],&quot;optionalPlugins&quot;:[]},&quot;config&quot;:{}},{&quot;id&quot;:&quot;management&quot;,&quot;plugin&quot;:{&quot;id&quot;:&quot;management&quot;,&quot;configPath&quot;:&quot;management&quot;,&quot;requiredPlugins&quot;:[&quot;kibana_legacy&quot;],&quot;optionalPlugins&quot;:[]},&quot;config&quot;:{}},{&quot;id&quot;:&quot;dev_tools&quot;,&quot;plugin&quot;:{&quot;id&quot;:&quot;dev_tools&quot;,&quot;configPath&quot;:&quot;dev_tools&quot;,&quot;requiredPlugins&quot;:[&quot;kibana_legacy&quot;],&quot;optionalPlugins&quot;:[]},&quot;config&quot;:{}},{&quot;id&quot;:&quot;home&quot;,&quot;plugin&quot;:{&quot;id&quot;:&quot;home&quot;,&quot;configPath&quot;:&quot;home&quot;,&quot;requiredPlugins&quot;:[],&quot;optionalPlugins&quot;:[]},&quot;config&quot;:{}},{&quot;id&quot;:&quot;cloud&quot;,&quot;plugin&quot;:{&quot;id&quot;:&quot;cloud&quot;,&quot;configPath&quot;:[&quot;xpack&quot;,&quot;cloud&quot;],&quot;requiredPlugins&quot;:[],&quot;optionalPlugins&quot;:[&quot;usageCollection&quot;,&quot;home&quot;]},&quot;config&quot;:{}},{&quot;id&quot;:&quot;graph&quot;,&quot;plugin&quot;:{&quot;id&quot;:&quot;graph&quot;,&quot;configPath&quot;:&quot;graph&quot;,&quot;requiredPlugins&quot;:[&quot;licensing&quot;],&quot;optionalPlugins&quot;:[&quot;home&quot;]},&quot;config&quot;:{}},{&quot;id&quot;:&quot;inspector&quot;,&quot;plugin&quot;:{&quot;id&quot;:&quot;inspector&quot;,&quot;configPath&quot;:&quot;inspector&quot;,&quot;requiredPlugins&quot;:[],&quot;optionalPlugins&quot;:[]},&quot;config&quot;:{}},{&quot;id&quot;:&quot;expressions&quot;,&quot;plugin&quot;:{&quot;id&quot;:&quot;expressions&quot;,&quot;configPath&quot;:&quot;expressions&quot;,&quot;requiredPlugins&quot;:[&quot;inspector&quot;],&quot;optionalPlugins&quot;:[]},&quot;config&quot;:{}},{&quot;id&quot;:&quot;visualizations&quot;,&quot;plugin&quot;:{&quot;id&quot;:&quot;visualizations&quot;,&quot;configPath&quot;:&quot;visualizations&quot;,&quot;requiredPlugins&quot;:[&quot;expressions&quot;],&quot;optionalPlugins&quot;:[]},&quot;config&quot;:{}},{&quot;id&quot;:&quot;embeddable&quot;,&quot;plugin&quot;:{&quot;id&quot;:&quot;embeddable&quot;,&quot;configPath&quot;:&quot;embeddable&quot;,&quot;requiredPlugins&quot;:[&quot;inspector&quot;,&quot;uiActions&quot;],&quot;optionalPlugins&quot;:[]},&quot;config&quot;:{}},{&quot;id&quot;:&quot;advancedUiActions&quot;,&quot;plugin&quot;:{&quot;id&quot;:&quot;advancedUiActions&quot;,&quot;configPath&quot;:&quot;advancedUiActions&quot;,&quot;requiredPlugins&quot;:[&quot;embeddable&quot;,&quot;uiActions&quot;],&quot;optionalPlugins&quot;:[]},&quot;config&quot;:{}},{&quot;id&quot;:&quot;dashboard_embeddable_container&quot;,&quot;plugin&quot;:{&quot;id&quot;:&quot;dashboard_embeddable_container&quot;,&quot;configPath&quot;:&quot;dashboard_embeddable_container&quot;,&quot;requiredPlugins&quot;:[&quot;embeddable&quot;,&quot;inspector&quot;,&quot;uiActions&quot;],&quot;optionalPlugins&quot;:[]},&quot;config&quot;:{}},{&quot;id&quot;:&quot;eui_utils&quot;,&quot;plugin&quot;:{&quot;id&quot;:&quot;eui_utils&quot;,&quot;configPath&quot;:&quot;eui_utils&quot;,&quot;requiredPlugins&quot;:[],&quot;optionalPlugins&quot;:[]},&quot;config&quot;:{}},{&quot;id&quot;:&quot;bfetch&quot;,&quot;plugin&quot;:{&quot;id&quot;:&quot;bfetch&quot;,&quot;configPath&quot;:&quot;bfetch&quot;,&quot;requiredPlugins&quot;:[],&quot;optionalPlugins&quot;:[]},&quot;config&quot;:{}}],&quot;legacyMetadata&quot;:{&quot;app&quot;:{&quot;id&quot;:&quot;kibana&quot;,&quot;title&quot;:&quot;Kibana&quot;,&quot;main&quot;:&quot;plugins/kibana/kibana&quot;,&quot;navLink&quot;:{&quot;id&quot;:&quot;kibana&quot;,&quot;title&quot;:&quot;Kibana&quot;,&quot;order&quot;:0,&quot;url&quot;:&quot;/app/kibana&quot;,&quot;subUrlBase&quot;:&quot;/app/kibana&quot;,&quot;linkToLastSubUrl&quot;:true,&quot;hidden&quot;:false,&quot;disabled&quot;:false,&quot;tooltip&quot;:&quot;&quot;},&quot;linkToLastSubUrl&quot;:true},&quot;bundleId&quot;:&quot;app:kibana&quot;,&quot;nav&quot;:[{&quot;id&quot;:&quot;kibana:discover&quot;,&quot;title&quot;:&quot;Discover&quot;,&quot;order&quot;:-1003,&quot;url&quot;:&quot;/app/kibana#/discover&quot;,&quot;subUrlBase&quot;:&quot;/app/kibana#/discover&quot;,&quot;euiIconType&quot;:&quot;discoverApp&quot;,&quot;linkToLastSubUrl&quot;:true,&quot;hidden&quot;:false,&quot;disabled&quot;:false,&quot;tooltip&quot;:&quot;&quot;},{&quot;id&quot;:&quot;kibana:visualize&quot;,&quot;title&quot;:&quot;Visualize&quot;,&quot;order&quot;:-1002,&quot;url&quot;:&quot;/app/kibana#/visualize&quot;,&quot;subUrlBase&quot;:&quot;/app/kibana#/visualize&quot;,&quot;euiIconType&quot;:&quot;visualizeApp&quot;,&quot;linkToLastSubUrl&quot;:true,&quot;hidden&quot;:false,&quot;disabled&quot;:false,&quot;tooltip&quot;:&quot;&quot;},{&quot;id&quot;:&quot;kibana:dashboard&quot;,&quot;title&quot;:&quot;Dashboard&quot;,&quot;order&quot;:-1001,&quot;url&quot;:&quot;/app/kibana#/dashboards&quot;,&quot;subUrlBase&quot;:&quot;/app/kibana#/dashboard&quot;,&quot;euiIconType&quot;:&quot;dashboardApp&quot;,&quot;linkToLastSubUrl&quot;:true,&quot;hidden&quot;:false,&quot;disabled&quot;:false,&quot;tooltip&quot;:&quot;&quot;},{&quot;id&quot;:&quot;timelion&quot;,&quot;title&quot;:&quot;Timelion&quot;,&quot;order&quot;:-1000,&quot;icon&quot;:&quot;plugins/timelion/icon.svg&quot;,&quot;euiIconType&quot;:&quot;timelionApp&quot;,&quot;url&quot;:&quot;/app/timelion&quot;,&quot;linkToLastSubUrl&quot;:true},{&quot;id&quot;:&quot;canvas&quot;,&quot;title&quot;:&quot;Canvas&quot;,&quot;order&quot;:0,&quot;icon&quot;:&quot;plugins/canvas/icon.svg&quot;,&quot;euiIconType&quot;:&quot;canvasApp&quot;,&quot;url&quot;:&quot;/app/canvas&quot;,&quot;linkToLastSubUrl&quot;:true},{&quot;id&quot;:&quot;maps&quot;,&quot;title&quot;:&quot;Maps&quot;,&quot;order&quot;:0,&quot;icon&quot;:&quot;plugins/maps/icon.svg&quot;,&quot;euiIconType&quot;:&quot;gisApp&quot;,&quot;url&quot;:&quot;/app/maps&quot;,&quot;linkToLastSubUrl&quot;:true},{&quot;id&quot;:&quot;ml&quot;,&quot;title&quot;:&quot;Machine Learning&quot;,&quot;order&quot;:0,&quot;icon&quot;:&quot;plugins/ml/application/ml.svg&quot;,&quot;euiIconType&quot;:&quot;machineLearningApp&quot;,&quot;url&quot;:&quot;/app/ml&quot;,&quot;linkToLastSubUrl&quot;:true},{&quot;id&quot;:&quot;infra:home&quot;,&quot;title&quot;:&quot;Metrics&quot;,&quot;order&quot;:8000,&quot;url&quot;:&quot;/app/infra#/infrastructure&quot;,&quot;subUrlBase&quot;:&quot;/app/infra#/infrastructure&quot;,&quot;icon&quot;:&quot;plugins/infra/images/infra_mono_white.svg&quot;,&quot;euiIconType&quot;:&quot;metricsApp&quot;,&quot;linkToLastSubUrl&quot;:true,&quot;hidden&quot;:false,&quot;disabled&quot;:false,&quot;tooltip&quot;:&quot;&quot;},{&quot;id&quot;:&quot;infra:logs&quot;,&quot;title&quot;:&quot;Logs&quot;,&quot;order&quot;:8001,&quot;url&quot;:&quot;/app/infra#/logs&quot;,&quot;subUrlBase&quot;:&quot;/app/infra#/logs&quot;,&quot;icon&quot;:&quot;plugins/infra/images/logging_mono_white.svg&quot;,&quot;euiIconType&quot;:&quot;logsApp&quot;,&quot;linkToLastSubUrl&quot;:true,&quot;hidden&quot;:false,&quot;disabled&quot;:false,&quot;tooltip&quot;:&quot;&quot;},{&quot;id&quot;:&quot;apm&quot;,&quot;title&quot;:&quot;APM&quot;,&quot;order&quot;:8100,&quot;icon&quot;:&quot;plugins/apm/icon.svg&quot;,&quot;euiIconType&quot;:&quot;apmApp&quot;,&quot;url&quot;:&quot;/app/apm&quot;,&quot;linkToLastSubUrl&quot;:true},{&quot;id&quot;:&quot;uptime&quot;,&quot;title&quot;:&quot;Uptime&quot;,&quot;order&quot;:8900,&quot;icon&quot;:&quot;plugins/uptime/icons/heartbeat_white.svg&quot;,&quot;euiIconType&quot;:&quot;uptimeApp&quot;,&quot;url&quot;:&quot;/app/uptime#/&quot;,&quot;linkToLastSubUrl&quot;:true},{&quot;id&quot;:&quot;siem&quot;,&quot;title&quot;:&quot;SIEM&quot;,&quot;order&quot;:9000,&quot;url&quot;:&quot;/app/siem&quot;,&quot;subUrlBase&quot;:&quot;/app/siem&quot;,&quot;euiIconType&quot;:&quot;securityAnalyticsApp&quot;,&quot;linkToLastSubUrl&quot;:true,&quot;hidden&quot;:false,&quot;disabled&quot;:false,&quot;tooltip&quot;:&quot;&quot;},{&quot;id&quot;:&quot;graph&quot;,&quot;title&quot;:&quot;Graph&quot;,&quot;order&quot;:9000,&quot;icon&quot;:&quot;plugins/graph/icon.png&quot;,&quot;euiIconType&quot;:&quot;graphApp&quot;,&quot;url&quot;:&quot;/app/graph&quot;,&quot;linkToLastSubUrl&quot;:true},{&quot;id&quot;:&quot;kibana:dev_tools&quot;,&quot;title&quot;:&quot;Dev Tools&quot;,&quot;order&quot;:9001,&quot;url&quot;:&quot;/app/kibana#/dev_tools&quot;,&quot;subUrlBase&quot;:&quot;/app/kibana#/dev_tools&quot;,&quot;euiIconType&quot;:&quot;devToolsApp&quot;,&quot;linkToLastSubUrl&quot;:true,&quot;hidden&quot;:false,&quot;disabled&quot;:false,&quot;tooltip&quot;:&quot;&quot;},{&quot;id&quot;:&quot;monitoring&quot;,&quot;title&quot;:&quot;Stack Monitoring&quot;,&quot;order&quot;:9002,&quot;icon&quot;:&quot;plugins/monitoring/icons/monitoring.svg&quot;,&quot;euiIconType&quot;:&quot;monitoringApp&quot;,&quot;url&quot;:&quot;/app/monitoring&quot;,&quot;linkToLastSubUrl&quot;:false},{&quot;id&quot;:&quot;kibana:management&quot;,&quot;title&quot;:&quot;Management&quot;,&quot;order&quot;:9003,&quot;url&quot;:&quot;/app/kibana#/management&quot;,&quot;subUrlBase&quot;:&quot;/app/kibana#/management&quot;,&quot;euiIconType&quot;:&quot;managementApp&quot;,&quot;linkToLastSubUrl&quot;:false,&quot;hidden&quot;:false,&quot;disabled&quot;:false,&quot;tooltip&quot;:&quot;&quot;}],&quot;version&quot;:&quot;7.6.1&quot;,&quot;branch&quot;:&quot;7.6&quot;,&quot;buildNum&quot;:29118,&quot;buildSha&quot;:&quot;5ddabf8510131ebf173762b7405e5e18f2757c12&quot;,&quot;devMode&quot;:false,&quot;basePath&quot;:&quot;&quot;,&quot;uiSettings&quot;:{&quot;defaults&quot;:{&quot;xPack:defaultAdminEmail&quot;:{&quot;name&quot;:&quot;Admin email&quot;,&quot;description&quot;:&quot;Recipient email address for X-Pack admin operations, such as Cluster Alert email notifications from Monitoring.&quot;,&quot;type&quot;:&quot;string&quot;,&quot;value&quot;:null},&quot;xpackDashboardMode:roles&quot;:{&quot;name&quot;:&quot;Dashboards only roles&quot;,&quot;description&quot;:&quot;Roles that belong to View Dashboards Only mode&quot;,&quot;value&quot;:[&quot;kibana_dashboard_only_user&quot;],&quot;category&quot;:[&quot;dashboard&quot;]},&quot;rollups:enableIndexPatterns&quot;:{&quot;name&quot;:&quot;Enable rollup index patterns&quot;,&quot;value&quot;:true,&quot;description&quot;:&quot;Enable the creation of index patterns which capture rollup indices,\n              which in turn enable visualizations based on rollup data. Refresh\n              the page to apply the changes.&quot;,&quot;category&quot;:[&quot;rollups&quot;]},&quot;siem:refreshIntervalDefaults&quot;:{&quot;type&quot;:&quot;json&quot;,&quot;name&quot;:&quot;Time filter refresh interval&quot;,&quot;value&quot;:&quot;{\n  \&quot;pause\&quot;: true,\n  \&quot;value\&quot;: 300000\n}&quot;,&quot;description&quot;:&quot;&lt;p&gt;Default refresh interval for the SIEM time filter, in milliseconds.&lt;/p&gt;&quot;,&quot;category&quot;:[&quot;siem&quot;],&quot;requiresPageReload&quot;:true},&quot;siem:timeDefaults&quot;:{&quot;type&quot;:&quot;json&quot;,&quot;name&quot;:&quot;Time filter period&quot;,&quot;value&quot;:&quot;{\n  \&quot;from\&quot;: \&quot;now-24h\&quot;,\n  \&quot;to\&quot;: \&quot;now\&quot;\n}&quot;,&quot;description&quot;:&quot;&lt;p&gt;Default period of time in the SIEM time filter.&lt;/p&gt;&quot;,&quot;category&quot;:[&quot;siem&quot;],&quot;requiresPageReload&quot;:true},&quot;siem:defaultIndex&quot;:{&quot;name&quot;:&quot;Elasticsearch indices&quot;,&quot;value&quot;:[&quot;apm-*-transaction*&quot;,&quot;auditbeat-*&quot;,&quot;endgame-*&quot;,&quot;filebeat-*&quot;,&quot;packetbeat-*&quot;,&quot;winlogbeat-*&quot;],&quot;description&quot;:&quot;&lt;p&gt;Comma-delimited list of Elasticsearch indices from which the SIEM app collects events.&lt;/p&gt;&quot;,&quot;category&quot;:[&quot;siem&quot;],&quot;requiresPageReload&quot;:true},&quot;siem:defaultAnomalyScore&quot;:{&quot;name&quot;:&quot;Anomaly threshold&quot;,&quot;value&quot;:50,&quot;type&quot;:&quot;number&quot;,&quot;description&quot;:&quot;&lt;p&gt;Value above which Machine Learning job anomalies are displayed in the SIEM app.&lt;/p&gt;&lt;p&gt;Valid values: 0 to 100.&lt;/p&gt;&quot;,&quot;category&quot;:[&quot;siem&quot;],&quot;requiresPageReload&quot;:true},&quot;siem:enableNewsFeed&quot;:{&quot;name&quot;:&quot;News feed&quot;,&quot;value&quot;:true,&quot;description&quot;:&quot;&lt;p&gt;Enables the News feed&lt;/p&gt;&quot;,&quot;type&quot;:&quot;boolean&quot;,&quot;category&quot;:[&quot;siem&quot;],&quot;requiresPageReload&quot;:true},&quot;siem:newsFeedUrl&quot;:{&quot;name&quot;:&quot;News feed URL&quot;,&quot;value&quot;:&quot;https://feeds.elastic.co/security-solution&quot;,&quot;description&quot;:&quot;&lt;p&gt;News feed content will be retrieved from this URL&lt;/p&gt;&quot;,&quot;category&quot;:[&quot;siem&quot;],&quot;requiresPageReload&quot;:true},&quot;buildNum&quot;:{&quot;readonly&quot;:true},&quot;defaultRoute&quot;:{&quot;name&quot;:&quot;Default route&quot;,&quot;value&quot;:&quot;/app/kibana&quot;,&quot;validation&quot;:{&quot;regexString&quot;:&quot;^/&quot;,&quot;message&quot;:&quot;The route must start with a slash (\&quot;/\&quot;)&quot;},&quot;description&quot;:&quot;This setting specifies the default route when opening Kibana. You can use this setting to modify the landing page when opening Kibana. The route must start with a slash (\&quot;/\&quot;).&quot;},&quot;query:queryString:options&quot;:{&quot;name&quot;:&quot;Query string options&quot;,&quot;value&quot;:&quot;{ \&quot;analyze_wildcard\&quot;: true }&quot;,&quot;description&quot;:&quot;&lt;a href=\&quot;https://www.elastic.co/guide/en/elasticsearch/reference/current/query-dsl-query-string-query.html\&quot; target=\&quot;_blank\&quot; rel=\&quot;noopener noreferrer\&quot;&gt;Options&lt;/a&gt; for the lucene query string parser. Is only used when \&quot;Query language\&quot; is set to Lucene.&quot;,&quot;type&quot;:&quot;json&quot;},&quot;query:allowLeadingWildcards&quot;:{&quot;name&quot;:&quot;Allow leading wildcards in query&quot;,&quot;value&quot;:true,&quot;description&quot;:&quot;When set, * is allowed as the first character in a query clause. Currently only applies when experimental query features are enabled in the query bar. To disallow leading wildcards in basic lucene queries, use query:queryString:options.&quot;},&quot;search:queryLanguage&quot;:{&quot;name&quot;:&quot;Query language&quot;,&quot;value&quot;:&quot;kuery&quot;,&quot;description&quot;:&quot;Query language used by the query bar. KQL is a new language built specifically for Kibana.&quot;,&quot;type&quot;:&quot;select&quot;,&quot;options&quot;:[&quot;lucene&quot;,&quot;kuery&quot;],&quot;optionLabels&quot;:{&quot;lucene&quot;:&quot;Lucene&quot;,&quot;kuery&quot;:&quot;KQL&quot;}},&quot;sort:options&quot;:{&quot;name&quot;:&quot;Sort options&quot;,&quot;value&quot;:&quot;{ \&quot;unmapped_type\&quot;: \&quot;boolean\&quot; }&quot;,&quot;description&quot;:&quot;&lt;a href=\&quot;https://www.elastic.co/guide/en/elasticsearch/reference/current/search-request-sort.html\&quot; target=\&quot;_blank\&quot; rel=\&quot;noopener noreferrer\&quot;&gt;Options&lt;/a&gt; for the Elasticsearch sort parameter&quot;,&quot;type&quot;:&quot;json&quot;},&quot;dateFormat&quot;:{&quot;name&quot;:&quot;Date format&quot;,&quot;value&quot;:&quot;MMM D, YYYY @ HH:mm:ss.SSS&quot;,&quot;description&quot;:&quot;When displaying a pretty formatted date, use this &lt;a href=\&quot;https://momentjs.com/docs/#/displaying/format/\&quot; target=\&quot;_blank\&quot; rel=\&quot;noopener noreferrer\&quot;&gt;format&lt;/a&gt;&quot;},&quot;dateFormat:tz&quot;:{&quot;name&quot;:&quot;Timezone for date formatting&quot;,&quot;value&quot;:&quot;Browser&quot;,&quot;description&quot;:&quot;Which timezone should be used. \&quot;Browser\&quot; will use the timezone detected by your browser.&quot;,&quot;type&quot;:&quot;select&quot;,&quot;options&quot;:[&quot;Browser&quot;,&quot;Africa/Abidjan&quot;,&quot;Africa/Accra&quot;,&quot;Africa/Addis_Ababa&quot;,&quot;Africa/Algiers&quot;,&quot;Africa/Asmara&quot;,&quot;Africa/Asmera&quot;,&quot;Africa/Bamako&quot;,&quot;Africa/Bangui&quot;,&quot;Africa/Banjul&quot;,&quot;Africa/Bissau&quot;,&quot;Africa/Blantyre&quot;,&quot;Africa/Brazzaville&quot;,&quot;Africa/Bujumbura&quot;,&quot;Africa/Cairo&quot;,&quot;Africa/Casablanca&quot;,&quot;Africa/Ceuta&quot;,&quot;Africa/Conakry&quot;,&quot;Africa/Dakar&quot;,&quot;Africa/Dar_es_Salaam&quot;,&quot;Africa/Djibouti&quot;,&quot;Africa/Douala&quot;,&quot;Africa/El_Aaiun&quot;,&quot;Africa/Freetown&quot;,&quot;Africa/Gaborone&quot;,&quot;Africa/Harare&quot;,&quot;Africa/Johannesburg&quot;,&quot;Africa/Juba&quot;,&quot;Africa/Kampala&quot;,&quot;Africa/Khartoum&quot;,&quot;Africa/Kigali&quot;,&quot;Africa/Kinshasa&quot;,&quot;Africa/Lagos&quot;,&quot;Africa/Libreville&quot;,&quot;Africa/Lome&quot;,&quot;Africa/Luanda&quot;,&quot;Africa/Lubumbashi&quot;,&quot;Africa/Lusaka&quot;,&quot;Africa/Malabo&quot;,&quot;Africa/Maputo&quot;,&quot;Africa/Maseru&quot;,&quot;Africa/Mbabane&quot;,&quot;Africa/Mogadishu&quot;,&quot;Africa/Monrovia&quot;,&quot;Africa/Nairobi&quot;,&quot;Africa/Ndjamena&quot;,&quot;Africa/Niamey&quot;,&quot;Africa/Nouakchott&quot;,&quot;Africa/Ouagadougou&quot;,&quot;Africa/Porto-Novo&quot;,&quot;Africa/Sao_Tome&quot;,&quot;Africa/Timbuktu&quot;,&quot;Africa/Tripoli&quot;,&quot;Africa/Tunis&quot;,&quot;Africa/Windhoek&quot;,&quot;America/Adak&quot;,&quot;America/Anchorage&quot;,&quot;America/Anguilla&quot;,&quot;America/Antigua&quot;,&quot;America/Araguaina&quot;,&quot;America/Argentina/Buenos_Aires&quot;,&quot;America/Argentina/Catamarca&quot;,&quot;America/Argentina/ComodRivadavia&quot;,&quot;America/Argentina/Cordoba&quot;,&quot;America/Argentina/Jujuy&quot;,&quot;America/Argentina/La_Rioja&quot;,&quot;America/Argentina/Mendoza&quot;,&quot;America/Argentina/Rio_Gallegos&quot;,&quot;America/Argentina/Salta&quot;,&quot;America/Argentina/San_Juan&quot;,&quot;America/Argentina/San_Luis&quot;,&quot;America/Argentina/Tucuman&quot;,&quot;America/Argentina/Ushuaia&quot;,&quot;America/Aruba&quot;,&quot;America/Asuncion&quot;,&quot;America/Atikokan&quot;,&quot;America/Atka&quot;,&quot;America/Bahia&quot;,&quot;America/Bahia_Banderas&quot;,&quot;America/Barbados&quot;,&quot;America/Belem&quot;,&quot;America/Belize&quot;,&quot;America/Blanc-Sablon&quot;,&quot;America/Boa_Vista&quot;,&quot;America/Bogota&quot;,&quot;America/Boise&quot;,&quot;America/Buenos_Aires&quot;,&quot;America/Cambridge_Bay&quot;,&quot;America/Campo_Grande&quot;,&quot;America/Cancun&quot;,&quot;America/Caracas&quot;,&quot;America/Catamarca&quot;,&quot;America/Cayenne&quot;,&quot;America/Cayman&quot;,&quot;America/Chicago&quot;,&quot;America/Chihuahua&quot;,&quot;America/Coral_Harbour&quot;,&quot;America/Cordoba&quot;,&quot;America/Costa_Rica&quot;,&quot;America/Creston&quot;,&quot;America/Cuiaba&quot;,&quot;America/Curacao&quot;,&quot;America/Danmarkshavn&quot;,&quot;America/Dawson&quot;,&quot;America/Dawson_Creek&quot;,&quot;America/Denver&quot;,&quot;America/Detroit&quot;,&quot;America/Dominica&quot;,&quot;America/Edmonton&quot;,&quot;America/Eirunepe&quot;,&quot;America/El_Salvador&quot;,&quot;America/Ensenada&quot;,&quot;America/Fort_Nelson&quot;,&quot;America/Fort_Wayne&quot;,&quot;America/Fortaleza&quot;,&quot;America/Glace_Bay&quot;,&quot;America/Godthab&quot;,&quot;America/Goose_Bay&quot;,&quot;America/Grand_Turk&quot;,&quot;America/Grenada&quot;,&quot;America/Guadeloupe&quot;,&quot;America/Guatemala&quot;,&quot;America/Guayaquil&quot;,&quot;America/Guyana&quot;,&quot;America/Halifax&quot;,&quot;America/Havana&quot;,&quot;America/Hermosillo&quot;,&quot;America/Indiana/Indianapolis&quot;,&quot;America/Indiana/Knox&quot;,&quot;America/Indiana/Marengo&quot;,&quot;America/Indiana/Petersburg&quot;,&quot;America/Indiana/Tell_City&quot;,&quot;America/Indiana/Vevay&quot;,&quot;America/Indiana/Vincennes&quot;,&quot;America/Indiana/Winamac&quot;,&quot;America/Indianapolis&quot;,&quot;America/Inuvik&quot;,&quot;America/Iqaluit&quot;,&quot;America/Jamaica&quot;,&quot;America/Jujuy&quot;,&quot;America/Juneau&quot;,&quot;America/Kentucky/Louisville&quot;,&quot;America/Kentucky/Monticello&quot;,&quot;America/Knox_IN&quot;,&quot;America/Kralendijk&quot;,&quot;America/La_Paz&quot;,&quot;America/Lima&quot;,&quot;America/Los_Angeles&quot;,&quot;America/Louisville&quot;,&quot;America/Lower_Princes&quot;,&quot;America/Maceio&quot;,&quot;America/Managua&quot;,&quot;America/Manaus&quot;,&quot;America/Marigot&quot;,&quot;America/Martinique&quot;,&quot;America/Matamoros&quot;,&quot;America/Mazatlan&quot;,&quot;America/Mendoza&quot;,&quot;America/Menominee&quot;,&quot;America/Merida&quot;,&quot;America/Metlakatla&quot;,&quot;America/Mexico_City&quot;,&quot;America/Miquelon&quot;,&quot;America/Moncton&quot;,&quot;America/Monterrey&quot;,&quot;America/Montevideo&quot;,&quot;America/Montreal&quot;,&quot;America/Montserrat&quot;,&quot;America/Nassau&quot;,&quot;America/New_York&quot;,&quot;America/Nipigon&quot;,&quot;America/Nome&quot;,&quot;America/Noronha&quot;,&quot;America/North_Dakota/Beulah&quot;,&quot;America/North_Dakota/Center&quot;,&quot;America/North_Dakota/New_Salem&quot;,&quot;America/Ojinaga&quot;,&quot;America/Panama&quot;,&quot;America/Pangnirtung&quot;,&quot;America/Paramaribo&quot;,&quot;America/Phoenix&quot;,&quot;America/Port-au-Prince&quot;,&quot;America/Port_of_Spain&quot;,&quot;America/Porto_Acre&quot;,&quot;America/Porto_Velho&quot;,&quot;America/Puerto_Rico&quot;,&quot;America/Punta_Arenas&quot;,&quot;America/Rainy_River&quot;,&quot;America/Rankin_Inlet&quot;,&quot;America/Recife&quot;,&quot;America/Regina&quot;,&quot;America/Resolute&quot;,&quot;America/Rio_Branco&quot;,&quot;America/Rosario&quot;,&quot;America/Santa_Isabel&quot;,&quot;America/Santarem&quot;,&quot;America/Santiago&quot;,&quot;America/Santo_Domingo&quot;,&quot;America/Sao_Paulo&quot;,&quot;America/Scoresbysund&quot;,&quot;America/Shiprock&quot;,&quot;America/Sitka&quot;,&quot;America/St_Barthelemy&quot;,&quot;America/St_Johns&quot;,&quot;America/St_Kitts&quot;,&quot;America/St_Lucia&quot;,&quot;America/St_Thomas&quot;,&quot;America/St_Vincent&quot;,&quot;America/Swift_Current&quot;,&quot;America/Tegucigalpa&quot;,&quot;America/Thule&quot;,&quot;America/Thunder_Bay&quot;,&quot;America/Tijuana&quot;,&quot;America/Toronto&quot;,&quot;America/Tortola&quot;,&quot;America/Vancouver&quot;,&quot;America/Virgin&quot;,&quot;America/Whitehorse&quot;,&quot;America/Winnipeg&quot;,&quot;America/Yakutat&quot;,&quot;America/Yellowknife&quot;,&quot;Antarctica/Casey&quot;,&quot;Antarctica/Davis&quot;,&quot;Antarctica/DumontDUrville&quot;,&quot;Antarctica/Macquarie&quot;,&quot;Antarctica/Mawson&quot;,&quot;Antarctica/McMurdo&quot;,&quot;Antarctica/Palmer&quot;,&quot;Antarctica/Rothera&quot;,&quot;Antarctica/South_Pole&quot;,&quot;Antarctica/Syowa&quot;,&quot;Antarctica/Troll&quot;,&quot;Antarctica/Vostok&quot;,&quot;Arctic/Longyearbyen&quot;,&quot;Asia/Aden&quot;,&quot;Asia/Almaty&quot;,&quot;Asia/Amman&quot;,&quot;Asia/Anadyr&quot;,&quot;Asia/Aqtau&quot;,&quot;Asia/Aqtobe&quot;,&quot;Asia/Ashgabat&quot;,&quot;Asia/Ashkhabad&quot;,&quot;Asia/Atyrau&quot;,&quot;Asia/Baghdad&quot;,&quot;Asia/Bahrain&quot;,&quot;Asia/Baku&quot;,&quot;Asia/Bangkok&quot;,&quot;Asia/Barnaul&quot;,&quot;Asia/Beirut&quot;,&quot;Asia/Bishkek&quot;,&quot;Asia/Brunei&quot;,&quot;Asia/Calcutta&quot;,&quot;Asia/Chita&quot;,&quot;Asia/Choibalsan&quot;,&quot;Asia/Chongqing&quot;,&quot;Asia/Chungking&quot;,&quot;Asia/Colombo&quot;,&quot;Asia/Dacca&quot;,&quot;Asia/Damascus&quot;,&quot;Asia/Dhaka&quot;,&quot;Asia/Dili&quot;,&quot;Asia/Dubai&quot;,&quot;Asia/Dushanbe&quot;,&quot;Asia/Famagusta&quot;,&quot;Asia/Gaza&quot;,&quot;Asia/Harbin&quot;,&quot;Asia/Hebron&quot;,&quot;Asia/Ho_Chi_Minh&quot;,&quot;Asia/Hong_Kong&quot;,&quot;Asia/Hovd&quot;,&quot;Asia/Irkutsk&quot;,&quot;Asia/Istanbul&quot;,&quot;Asia/Jakarta&quot;,&quot;Asia/Jayapura&quot;,&quot;Asia/Jerusalem&quot;,&quot;Asia/Kabul&quot;,&quot;Asia/Kamchatka&quot;,&quot;Asia/Karachi&quot;,&quot;Asia/Kashgar&quot;,&quot;Asia/Kathmandu&quot;,&quot;Asia/Katmandu&quot;,&quot;Asia/Khandyga&quot;,&quot;Asia/Kolkata&quot;,&quot;Asia/Krasnoyarsk&quot;,&quot;Asia/Kuala_Lumpur&quot;,&quot;Asia/Kuching&quot;,&quot;Asia/Kuwait&quot;,&quot;Asia/Macao&quot;,&quot;Asia/Macau&quot;,&quot;Asia/Magadan&quot;,&quot;Asia/Makassar&quot;,&quot;Asia/Manila&quot;,&quot;Asia/Muscat&quot;,&quot;Asia/Nicosia&quot;,&quot;Asia/Novokuznetsk&quot;,&quot;Asia/Novosibirsk&quot;,&quot;Asia/Omsk&quot;,&quot;Asia/Oral&quot;,&quot;Asia/Phnom_Penh&quot;,&quot;Asia/Pontianak&quot;,&quot;Asia/Pyongyang&quot;,&quot;Asia/Qatar&quot;,&quot;Asia/Qostanay&quot;,&quot;Asia/Qyzylorda&quot;,&quot;Asia/Rangoon&quot;,&quot;Asia/Riyadh&quot;,&quot;Asia/Saigon&quot;,&quot;Asia/Sakhalin&quot;,&quot;Asia/Samarkand&quot;,&quot;Asia/Seoul&quot;,&quot;Asia/Shanghai&quot;,&quot;Asia/Singapore&quot;,&quot;Asia/Srednekolymsk&quot;,&quot;Asia/Taipei&quot;,&quot;Asia/Tashkent&quot;,&quot;Asia/Tbilisi&quot;,&quot;Asia/Tehran&quot;,&quot;Asia/Tel_Aviv&quot;,&quot;Asia/Thimbu&quot;,&quot;Asia/Thimphu&quot;,&quot;Asia/Tokyo&quot;,&quot;Asia/Tomsk&quot;,&quot;Asia/Ujung_Pandang&quot;,&quot;Asia/Ulaanbaatar&quot;,&quot;Asia/Ulan_Bator&quot;,&quot;Asia/Urumqi&quot;,&quot;Asia/Ust-Nera&quot;,&quot;Asia/Vientiane&quot;,&quot;Asia/Vladivostok&quot;,&quot;Asia/Yakutsk&quot;,&quot;Asia/Yangon&quot;,&quot;Asia/Yekaterinburg&quot;,&quot;Asia/Yerevan&quot;,&quot;Atlantic/Azores&quot;,&quot;Atlantic/Bermuda&quot;,&quot;Atlantic/Canary&quot;,&quot;Atlantic/Cape_Verde&quot;,&quot;Atlantic/Faeroe&quot;,&quot;Atlantic/Faroe&quot;,&quot;Atlantic/Jan_Mayen&quot;,&quot;Atlantic/Madeira&quot;,&quot;Atlantic/Reykjavik&quot;,&quot;Atlantic/South_Georgia&quot;,&quot;Atlantic/St_Helena&quot;,&quot;Atlantic/Stanley&quot;,&quot;Australia/ACT&quot;,&quot;Australia/Adelaide&quot;,&quot;Australia/Brisbane&quot;,&quot;Australia/Broken_Hill&quot;,&quot;Australia/Canberra&quot;,&quot;Australia/Currie&quot;,&quot;Australia/Darwin&quot;,&quot;Australia/Eucla&quot;,&quot;Australia/Hobart&quot;,&quot;Australia/LHI&quot;,&quot;Australia/Lindeman&quot;,&quot;Australia/Lord_Howe&quot;,&quot;Australia/Melbourne&quot;,&quot;Australia/NSW&quot;,&quot;Australia/North&quot;,&quot;Australia/Perth&quot;,&quot;Australia/Queensland&quot;,&quot;Australia/South&quot;,&quot;Australia/Sydney&quot;,&quot;Australia/Tasmania&quot;,&quot;Australia/Victoria&quot;,&quot;Australia/West&quot;,&quot;Australia/Yancowinna&quot;,&quot;Brazil/Acre&quot;,&quot;Brazil/DeNoronha&quot;,&quot;Brazil/East&quot;,&quot;Brazil/West&quot;,&quot;CET&quot;,&quot;CST6CDT&quot;,&quot;Canada/Atlantic&quot;,&quot;Canada/Central&quot;,&quot;Canada/Eastern&quot;,&quot;Canada/Mountain&quot;,&quot;Canada/Newfoundland&quot;,&quot;Canada/Pacific&quot;,&quot;Canada/Saskatchewan&quot;,&quot;Canada/Yukon&quot;,&quot;Chile/Continental&quot;,&quot;Chile/EasterIsland&quot;,&quot;Cuba&quot;,&quot;EET&quot;,&quot;EST&quot;,&quot;EST5EDT&quot;,&quot;Egypt&quot;,&quot;Eire&quot;,&quot;Etc/GMT&quot;,&quot;Etc/GMT+0&quot;,&quot;Etc/GMT+1&quot;,&quot;Etc/GMT+10&quot;,&quot;Etc/GMT+11&quot;,&quot;Etc/GMT+12&quot;,&quot;Etc/GMT+2&quot;,&quot;Etc/GMT+3&quot;,&quot;Etc/GMT+4&quot;,&quot;Etc/GMT+5&quot;,&quot;Etc/GMT+6&quot;,&quot;Etc/GMT+7&quot;,&quot;Etc/GMT+8&quot;,&quot;Etc/GMT+9&quot;,&quot;Etc/GMT-0&quot;,&quot;Etc/GMT-1&quot;,&quot;Etc/GMT-10&quot;,&quot;Etc/GMT-11&quot;,&quot;Etc/GMT-12&quot;,&quot;Etc/GMT-13&quot;,&quot;Etc/GMT-14&quot;,&quot;Etc/GMT-2&quot;,&quot;Etc/GMT-3&quot;,&quot;Etc/GMT-4&quot;,&quot;Etc/GMT-5&quot;,&quot;Etc/GMT-6&quot;,&quot;Etc/GMT-7&quot;,&quot;Etc/GMT-8&quot;,&quot;Etc/GMT-9&quot;,&quot;Etc/GMT0&quot;,&quot;Etc/Greenwich&quot;,&quot;Etc/UCT&quot;,&quot;Etc/UTC&quot;,&quot;Etc/Universal&quot;,&quot;Etc/Zulu&quot;,&quot;Europe/Amsterdam&quot;,&quot;Europe/Andorra&quot;,&quot;Europe/Astrakhan&quot;,&quot;Europe/Athens&quot;,&quot;Europe/Belfast&quot;,&quot;Europe/Belgrade&quot;,&quot;Europe/Berlin&quot;,&quot;Europe/Bratislava&quot;,&quot;Europe/Brussels&quot;,&quot;Europe/Bucharest&quot;,&quot;Europe/Budapest&quot;,&quot;Europe/Busingen&quot;,&quot;Europe/Chisinau&quot;,&quot;Europe/Copenhagen&quot;,&quot;Europe/Dublin&quot;,&quot;Europe/Gibraltar&quot;,&quot;Europe/Guernsey&quot;,&quot;Europe/Helsinki&quot;,&quot;Europe/Isle_of_Man&quot;,&quot;Europe/Istanbul&quot;,&quot;Europe/Jersey&quot;,&quot;Europe/Kaliningrad&quot;,&quot;Europe/Kiev&quot;,&quot;Europe/Kirov&quot;,&quot;Europe/Lisbon&quot;,&quot;Europe/Ljubljana&quot;,&quot;Europe/London&quot;,&quot;Europe/Luxembourg&quot;,&quot;Europe/Madrid&quot;,&quot;Europe/Malta&quot;,&quot;Europe/Mariehamn&quot;,&quot;Europe/Minsk&quot;,&quot;Europe/Monaco&quot;,&quot;Europe/Moscow&quot;,&quot;Europe/Nicosia&quot;,&quot;Europe/Oslo&quot;,&quot;Europe/Paris&quot;,&quot;Europe/Podgorica&quot;,&quot;Europe/Prague&quot;,&quot;Europe/Riga&quot;,&quot;Europe/Rome&quot;,&quot;Europe/Samara&quot;,&quot;Europe/San_Marino&quot;,&quot;Europe/Sarajevo&quot;,&quot;Europe/Saratov&quot;,&quot;Europe/Simferopol&quot;,&quot;Europe/Skopje&quot;,&quot;Europe/Sofia&quot;,&quot;Europe/Stockholm&quot;,&quot;Europe/Tallinn&quot;,&quot;Europe/Tirane&quot;,&quot;Europe/Tiraspol&quot;,&quot;Europe/Ulyanovsk&quot;,&quot;Europe/Uzhgorod&quot;,&quot;Europe/Vaduz&quot;,&quot;Europe/Vatican&quot;,&quot;Europe/Vienna&quot;,&quot;Europe/Vilnius&quot;,&quot;Europe/Volgograd&quot;,&quot;Europe/Warsaw&quot;,&quot;Europe/Zagreb&quot;,&quot;Europe/Zaporozhye&quot;,&quot;Europe/Zurich&quot;,&quot;GB&quot;,&quot;GB-Eire&quot;,&quot;GMT&quot;,&quot;GMT+0&quot;,&quot;GMT-0&quot;,&quot;GMT0&quot;,&quot;Greenwich&quot;,&quot;HST&quot;,&quot;Hongkong&quot;,&quot;Iceland&quot;,&quot;Indian/Antananarivo&quot;,&quot;Indian/Chagos&quot;,&quot;Indian/Christmas&quot;,&quot;Indian/Cocos&quot;,&quot;Indian/Comoro&quot;,&quot;Indian/Kerguelen&quot;,&quot;Indian/Mahe&quot;,&quot;Indian/Maldives&quot;,&quot;Indian/Mauritius&quot;,&quot;Indian/Mayotte&quot;,&quot;Indian/Reunion&quot;,&quot;Iran&quot;,&quot;Israel&quot;,&quot;Jamaica&quot;,&quot;Japan&quot;,&quot;Kwajalein&quot;,&quot;Libya&quot;,&quot;MET&quot;,&quot;MST&quot;,&quot;MST7MDT&quot;,&quot;Mexico/BajaNorte&quot;,&quot;Mexico/BajaSur&quot;,&quot;Mexico/General&quot;,&quot;NZ&quot;,&quot;NZ-CHAT&quot;,&quot;Navajo&quot;,&quot;PRC&quot;,&quot;PST8PDT&quot;,&quot;Pacific/Apia&quot;,&quot;Pacific/Auckland&quot;,&quot;Pacific/Bougainville&quot;,&quot;Pacific/Chatham&quot;,&quot;Pacific/Chuuk&quot;,&quot;Pacific/Easter&quot;,&quot;Pacific/Efate&quot;,&quot;Pacific/Enderbury&quot;,&quot;Pacific/Fakaofo&quot;,&quot;Pacific/Fiji&quot;,&quot;Pacific/Funafuti&quot;,&quot;Pacific/Galapagos&quot;,&quot;Pacific/Gambier&quot;,&quot;Pacific/Guadalcanal&quot;,&quot;Pacific/Guam&quot;,&quot;Pacific/Honolulu&quot;,&quot;Pacific/Johnston&quot;,&quot;Pacific/Kiritimati&quot;,&quot;Pacific/Kosrae&quot;,&quot;Pacific/Kwajalein&quot;,&quot;Pacific/Majuro&quot;,&quot;Pacific/Marquesas&quot;,&quot;Pacific/Midway&quot;,&quot;Pacific/Nauru&quot;,&quot;Pacific/Niue&quot;,&quot;Pacific/Norfolk&quot;,&quot;Pacific/Noumea&quot;,&quot;Pacific/Pago_Pago&quot;,&quot;Pacific/Palau&quot;,&quot;Pacific/Pitcairn&quot;,&quot;Pacific/Pohnpei&quot;,&quot;Pacific/Ponape&quot;,&quot;Pacific/Port_Moresby&quot;,&quot;Pacific/Rarotonga&quot;,&quot;Pacific/Saipan&quot;,&quot;Pacific/Samoa&quot;,&quot;Pacific/Tahiti&quot;,&quot;Pacific/Tarawa&quot;,&quot;Pacific/Tongatapu&quot;,&quot;Pacific/Truk&quot;,&quot;Pacific/Wake&quot;,&quot;Pacific/Wallis&quot;,&quot;Pacific/Yap&quot;,&quot;Poland&quot;,&quot;Portugal&quot;,&quot;ROC&quot;,&quot;ROK&quot;,&quot;Singapore&quot;,&quot;Turkey&quot;,&quot;UCT&quot;,&quot;US/Alaska&quot;,&quot;US/Aleutian&quot;,&quot;US/Arizona&quot;,&quot;US/Central&quot;,&quot;US/East-Indiana&quot;,&quot;US/Eastern&quot;,&quot;US/Hawaii&quot;,&quot;US/Indiana-Starke&quot;,&quot;US/Michigan&quot;,&quot;US/Mountain&quot;,&quot;US/Pacific&quot;,&quot;US/Pacific-New&quot;,&quot;US/Samoa&quot;,&quot;UTC&quot;,&quot;Universal&quot;,&quot;W-SU&quot;,&quot;WET&quot;,&quot;Zulu&quot;],&quot;requiresPageReload&quot;:true},&quot;dateFormat:scaled&quot;:{&quot;name&quot;:&quot;Scaled date format&quot;,&quot;type&quot;:&quot;json&quot;,&quot;value&quot;:&quot;[\n  [\&quot;\&quot;, \&quot;HH:mm:ss.SSS\&quot;],\n  [\&quot;PT1S\&quot;, \&quot;HH:mm:ss\&quot;],\n  [\&quot;PT1M\&quot;, \&quot;HH:mm\&quot;],\n  [\&quot;PT1H\&quot;, \&quot;YYYY-MM-DD HH:mm\&quot;],\n  [\&quot;P1DT\&quot;, \&quot;YYYY-MM-DD\&quot;],\n  [\&quot;P1YT\&quot;, \&quot;YYYY\&quot;]\n]&quot;,&quot;description&quot;:&quot;Values that define the format used in situations where time-based data is rendered in order, and formatted timestamps should adapt to the interval between measurements. Keys are &lt;a href=\&quot;http://en.wikipedia.org/wiki/ISO_8601#Time_intervals\&quot; target=\&quot;_blank\&quot; rel=\&quot;noopener noreferrer\&quot;&gt;ISO8601 intervals&lt;/a&gt;.&quot;},&quot;dateFormat:dow&quot;:{&quot;name&quot;:&quot;Day of week&quot;,&quot;value&quot;:&quot;Sunday&quot;,&quot;description&quot;:&quot;What day should weeks start on?&quot;,&quot;type&quot;:&quot;select&quot;,&quot;options&quot;:[&quot;Sunday&quot;,&quot;Monday&quot;,&quot;Tuesday&quot;,&quot;Wednesday&quot;,&quot;Thursday&quot;,&quot;Friday&quot;,&quot;Saturday&quot;]},&quot;dateNanosFormat&quot;:{&quot;name&quot;:&quot;Date with nanoseconds format&quot;,&quot;value&quot;:&quot;MMM D, YYYY @ HH:mm:ss.SSSSSSSSS&quot;,&quot;description&quot;:&quot;Used for the &lt;a href=\&quot;https://www.elastic.co/guide/en/elasticsearch/reference/master/date_nanos.html\&quot; target=\&quot;_blank\&quot; rel=\&quot;noopener noreferrer\&quot;&gt;date_nanos&lt;/a&gt; datatype of Elasticsearch&quot;},&quot;defaultIndex&quot;:{&quot;name&quot;:&quot;Default index&quot;,&quot;value&quot;:null,&quot;description&quot;:&quot;The index to access if no index is set&quot;},&quot;defaultColumns&quot;:{&quot;name&quot;:&quot;Default columns&quot;,&quot;value&quot;:[&quot;_source&quot;],&quot;description&quot;:&quot;Columns displayed by default in the Discovery tab&quot;,&quot;category&quot;:[&quot;discover&quot;]},&quot;metaFields&quot;:{&quot;name&quot;:&quot;Meta fields&quot;,&quot;value&quot;:[&quot;_source&quot;,&quot;_id&quot;,&quot;_type&quot;,&quot;_index&quot;,&quot;_score&quot;],&quot;description&quot;:&quot;Fields that exist outside of _source to merge into our document when displaying it&quot;},&quot;discover:sampleSize&quot;:{&quot;name&quot;:&quot;Number of rows&quot;,&quot;value&quot;:500,&quot;description&quot;:&quot;The number of rows to show in the table&quot;,&quot;category&quot;:[&quot;discover&quot;]},&quot;discover:aggs:terms:size&quot;:{&quot;name&quot;:&quot;Number of terms&quot;,&quot;value&quot;:20,&quot;type&quot;:&quot;number&quot;,&quot;description&quot;:&quot;Determines how many terms will be visualized when clicking the \&quot;visualize\&quot; button, in the field drop downs, in the discover sidebar.&quot;,&quot;category&quot;:[&quot;discover&quot;]},&quot;discover:sort:defaultOrder&quot;:{&quot;name&quot;:&quot;Default sort direction&quot;,&quot;value&quot;:&quot;desc&quot;,&quot;options&quot;:[&quot;desc&quot;,&quot;asc&quot;],&quot;optionLabels&quot;:{&quot;desc&quot;:&quot;Descending&quot;,&quot;asc&quot;:&quot;Ascending&quot;},&quot;type&quot;:&quot;select&quot;,&quot;description&quot;:&quot;Controls the default sort direction for time based index patterns in the Discover app.&quot;,&quot;category&quot;:[&quot;discover&quot;]},&quot;discover:searchOnPageLoad&quot;:{&quot;name&quot;:&quot;Search on page load&quot;,&quot;value&quot;:true,&quot;type&quot;:&quot;boolean&quot;,&quot;description&quot;:&quot;Controls whether a search is executed when Discover first loads. This setting does not have an effect when loading a saved search.&quot;,&quot;category&quot;:[&quot;discover&quot;]},&quot;doc_table:highlight&quot;:{&quot;name&quot;:&quot;Highlight results&quot;,&quot;value&quot;:true,&quot;description&quot;:&quot;Highlight results in Discover and Saved Searches Dashboard. Highlighting makes requests slow when working on big documents.&quot;,&quot;category&quot;:[&quot;discover&quot;]},&quot;doc_table:hideTimeColumn&quot;:{&quot;name&quot;:&quot;Hide &#x27;Time&#x27; column&quot;,&quot;value&quot;:false,&quot;description&quot;:&quot;Hide the &#x27;Time&#x27; column in Discover and in all Saved Searches on Dashboards.&quot;,&quot;category&quot;:[&quot;discover&quot;]},&quot;courier:ignoreFilterIfFieldNotInIndex&quot;:{&quot;name&quot;:&quot;Ignore filter(s)&quot;,&quot;value&quot;:false,&quot;description&quot;:&quot;This configuration enhances support for dashboards containing visualizations accessing dissimilar indexes. When disabled, all filters are applied to all visualizations. When enabled, filter(s) will be ignored for a visualization when the visualization&#x27;s index does not contain the filtering field.&quot;,&quot;category&quot;:[&quot;search&quot;]},&quot;courier:setRequestPreference&quot;:{&quot;name&quot;:&quot;Request preference&quot;,&quot;value&quot;:&quot;sessionId&quot;,&quot;options&quot;:[&quot;sessionId&quot;,&quot;custom&quot;,&quot;none&quot;],&quot;optionLabels&quot;:{&quot;sessionId&quot;:&quot;Session ID&quot;,&quot;custom&quot;:&quot;Custom&quot;,&quot;none&quot;:&quot;None&quot;},&quot;type&quot;:&quot;select&quot;,&quot;description&quot;:&quot;Allows you to set which shards handle your search requests.\n          &lt;ul&gt;\n            &lt;li&gt;&lt;strong&gt;Session ID:&lt;/strong&gt; restricts operations to execute all search requests on the same shards.\n              This has the benefit of reusing shard caches across requests.&lt;/li&gt;\n            &lt;li&gt;&lt;strong&gt;Custom:&lt;/strong&gt; allows you to define a your own preference.\n              Use &lt;strong&gt;courier:customRequestPreference&lt;/strong&gt; to customize your preference value.&lt;/li&gt;\n            &lt;li&gt;&lt;strong&gt;None:&lt;/strong&gt; means do not set a preference.\n              This might provide better performance because requests can be spread across all shard copies.\n              However, results might be inconsistent because different shards might be in different refresh states.&lt;/li&gt;\n          &lt;/ul&gt;&quot;,&quot;category&quot;:[&quot;search&quot;]},&quot;courier:customRequestPreference&quot;:{&quot;name&quot;:&quot;Custom request preference&quot;,&quot;value&quot;:&quot;_local&quot;,&quot;type&quot;:&quot;string&quot;,&quot;description&quot;:&quot;&lt;a href=\&quot;https://www.elastic.co/guide/en/elasticsearch/reference/current/search-request-preference.html\&quot; target=\&quot;_blank\&quot; rel=\&quot;noopener noreferrer\&quot;&gt;Request Preference&lt;/a&gt; used when &lt;strong&gt;courier:setRequestPreference&lt;/strong&gt; is set to \&quot;custom\&quot;.&quot;,&quot;category&quot;:[&quot;search&quot;]},&quot;courier:maxConcurrentShardRequests&quot;:{&quot;name&quot;:&quot;Max Concurrent Shard Requests&quot;,&quot;value&quot;:0,&quot;type&quot;:&quot;number&quot;,&quot;description&quot;:&quot;Controls the &lt;a href=\&quot;https://www.elastic.co/guide/en/elasticsearch/reference/current/search-multi-search.html\&quot;\n            target=\&quot;_blank\&quot; rel=\&quot;noopener noreferrer\&quot; &gt;max_concurrent_shard_requests&lt;/a&gt; setting used for _msearch requests sent by Kibana. Set to 0 to disable this config and use the Elasticsearch default.&quot;,&quot;category&quot;:[&quot;search&quot;]},&quot;courier:batchSearches&quot;:{&quot;name&quot;:&quot;Batch concurrent searches&quot;,&quot;value&quot;:false,&quot;type&quot;:&quot;boolean&quot;,&quot;description&quot;:&quot;When disabled, dashboard panels will load individually, and search requests will terminate when users navigate\n           away or update the query. When enabled, dashboard panels will load together when all of the data is loaded, and\n           searches will not terminate.&quot;,&quot;deprecation&quot;:{&quot;message&quot;:&quot;This setting is deprecated and will be removed in Kibana 8.0.&quot;,&quot;docLinksKey&quot;:&quot;kibanaSearchSettings&quot;},&quot;category&quot;:[&quot;search&quot;]},&quot;search:includeFrozen&quot;:{&quot;name&quot;:&quot;Search in frozen indices&quot;,&quot;description&quot;:&quot;Will include &lt;a href=\&quot;https://www.elastic.co/guide/en/elasticsearch/reference/current/frozen-indices.html\&quot;\n        target=\&quot;_blank\&quot; rel=\&quot;noopener noreferrer\&quot;&gt;frozen indices&lt;/a&gt; in results if enabled. Searching through frozen indices\n        might increase the search time.&quot;,&quot;value&quot;:false,&quot;category&quot;:[&quot;search&quot;]},&quot;fields:popularLimit&quot;:{&quot;name&quot;:&quot;Popular fields limit&quot;,&quot;value&quot;:10,&quot;description&quot;:&quot;The top N most popular fields to show&quot;},&quot;histogram:barTarget&quot;:{&quot;name&quot;:&quot;Target bars&quot;,&quot;value&quot;:50,&quot;description&quot;:&quot;Attempt to generate around this many bars when using \&quot;auto\&quot; interval in date histograms&quot;},&quot;histogram:maxBars&quot;:{&quot;name&quot;:&quot;Maximum bars&quot;,&quot;value&quot;:100,&quot;description&quot;:&quot;Never show more than this many bars in date histograms, scale values if needed&quot;},&quot;visualize:enableLabs&quot;:{&quot;name&quot;:&quot;Enable experimental visualizations&quot;,&quot;value&quot;:true,&quot;description&quot;:&quot;Allows users to create, view, and edit experimental visualizations. If disabled,\n          only visualizations that are considered production-ready are available to the user.&quot;,&quot;category&quot;:[&quot;visualization&quot;]},&quot;visualization:tileMap:maxPrecision&quot;:{&quot;name&quot;:&quot;Maximum tile map precision&quot;,&quot;value&quot;:7,&quot;description&quot;:&quot;The maximum geoHash precision displayed on tile maps: 7 is high, 10 is very high, 12 is the max. &lt;a href=\&quot;http://www.elastic.co/guide/en/elasticsearch/reference/current/search-aggregations-bucket-geohashgrid-aggregation.html#_cell_dimensions_at_the_equator\&quot;\n            target=\&quot;_blank\&quot; rel=\&quot;noopener noreferrer\&quot;&gt;Explanation of cell dimensions&lt;/a&gt;&quot;,&quot;category&quot;:[&quot;visualization&quot;]},&quot;visualization:tileMap:WMSdefaults&quot;:{&quot;name&quot;:&quot;Default WMS properties&quot;,&quot;value&quot;:&quot;{\n  \&quot;enabled\&quot;: false,\n  \&quot;options\&quot;: {\n    \&quot;format\&quot;: \&quot;image/png\&quot;,\n    \&quot;transparent\&quot;: true\n  }\n}&quot;,&quot;type&quot;:&quot;json&quot;,&quot;description&quot;:&quot;Default &lt;a href=\&quot;http://leafletjs.com/reference.html#tilelayer-wms\&quot; target=\&quot;_blank\&quot; rel=\&quot;noopener noreferrer\&quot;&gt;properties&lt;/a&gt; for the WMS map server support in the coordinate map&quot;,&quot;category&quot;:[&quot;visualization&quot;]},&quot;visualization:regionmap:showWarnings&quot;:{&quot;name&quot;:&quot;Show region map warning&quot;,&quot;value&quot;:true,&quot;description&quot;:&quot;Whether the region map shows a warning when terms cannot be joined to a shape on the map.&quot;,&quot;category&quot;:[&quot;visualization&quot;]},&quot;visualization:colorMapping&quot;:{&quot;name&quot;:&quot;Color mapping&quot;,&quot;value&quot;:&quot;{\&quot;Count\&quot;:\&quot;#00A69B\&quot;}&quot;,&quot;type&quot;:&quot;json&quot;,&quot;description&quot;:&quot;Maps values to specified colors within visualizations&quot;,&quot;category&quot;:[&quot;visualization&quot;]},&quot;visualization:loadingDelay&quot;:{&quot;name&quot;:&quot;Loading delay&quot;,&quot;value&quot;:&quot;2s&quot;,&quot;description&quot;:&quot;Time to wait before dimming visualizations during query&quot;,&quot;category&quot;:[&quot;visualization&quot;]},&quot;visualization:dimmingOpacity&quot;:{&quot;name&quot;:&quot;Dimming opacity&quot;,&quot;value&quot;:0.5,&quot;type&quot;:&quot;number&quot;,&quot;description&quot;:&quot;The opacity of the chart items that are dimmed when highlighting another element of the chart. The lower this number, the more the highlighted element will stand out. This must be a number between 0 and 1.&quot;,&quot;category&quot;:[&quot;visualization&quot;]},&quot;visualization:heatmap:maxBuckets&quot;:{&quot;name&quot;:&quot;Heatmap maximum buckets&quot;,&quot;value&quot;:50,&quot;type&quot;:&quot;number&quot;,&quot;description&quot;:&quot;The maximum number of buckets a single datasource can return. A higher number might have negative impact on browser rendering performance&quot;,&quot;category&quot;:[&quot;visualization&quot;]},&quot;csv:separator&quot;:{&quot;name&quot;:&quot;CSV separator&quot;,&quot;value&quot;:&quot;,&quot;,&quot;description&quot;:&quot;Separate exported values with this string&quot;},&quot;csv:quoteValues&quot;:{&quot;name&quot;:&quot;Quote CSV values&quot;,&quot;value&quot;:true,&quot;description&quot;:&quot;Should values be quoted in csv exports?&quot;},&quot;history:limit&quot;:{&quot;name&quot;:&quot;History limit&quot;,&quot;value&quot;:10,&quot;description&quot;:&quot;In fields that have history (e.g. query inputs), show this many recent values&quot;},&quot;shortDots:enable&quot;:{&quot;name&quot;:&quot;Shorten fields&quot;,&quot;value&quot;:false,&quot;description&quot;:&quot;Shorten long fields, for example, instead of foo.bar.baz, show f.b.baz&quot;},&quot;truncate:maxHeight&quot;:{&quot;name&quot;:&quot;Maximum table cell height&quot;,&quot;value&quot;:115,&quot;description&quot;:&quot;The maximum height that a cell in a table should occupy. Set to 0 to disable truncation&quot;},&quot;indexPattern:fieldMapping:lookBack&quot;:{&quot;name&quot;:&quot;Recent matching patterns&quot;,&quot;value&quot;:5,&quot;description&quot;:&quot;For index patterns containing timestamps in their names, look for this many recent matching patterns from which to query the field mapping&quot;},&quot;format:defaultTypeMap&quot;:{&quot;name&quot;:&quot;Field type format name&quot;,&quot;value&quot;:&quot;{\n  \&quot;ip\&quot;: { \&quot;id\&quot;: \&quot;ip\&quot;, \&quot;params\&quot;: {} },\n  \&quot;date\&quot;: { \&quot;id\&quot;: \&quot;date\&quot;, \&quot;params\&quot;: {} },\n  \&quot;date_nanos\&quot;: { \&quot;id\&quot;: \&quot;date_nanos\&quot;, \&quot;params\&quot;: {}, \&quot;es\&quot;: true },\n  \&quot;number\&quot;: { \&quot;id\&quot;: \&quot;number\&quot;, \&quot;params\&quot;: {} },\n  \&quot;boolean\&quot;: { \&quot;id\&quot;: \&quot;boolean\&quot;, \&quot;params\&quot;: {} },\n  \&quot;_source\&quot;: { \&quot;id\&quot;: \&quot;_source\&quot;, \&quot;params\&quot;: {} },\n  \&quot;_default_\&quot;: { \&quot;id\&quot;: \&quot;string\&quot;, \&quot;params\&quot;: {} }\n}&quot;,&quot;type&quot;:&quot;json&quot;,&quot;description&quot;:&quot;Map of the format name to use by default for each field type. \&quot;_default_\&quot; is used if the field type is not mentioned explicitly&quot;},&quot;format:number:defaultPattern&quot;:{&quot;name&quot;:&quot;Number format&quot;,&quot;value&quot;:&quot;0,0.[000]&quot;,&quot;type&quot;:&quot;string&quot;,&quot;description&quot;:&quot;Default &lt;a href=\&quot;http://numeraljs.com/\&quot; target=\&quot;_blank\&quot; rel=\&quot;noopener noreferrer\&quot;&gt;numeral format&lt;/a&gt; for the \&quot;number\&quot; format&quot;},&quot;format:bytes:defaultPattern&quot;:{&quot;name&quot;:&quot;Bytes format&quot;,&quot;value&quot;:&quot;0,0.[0]b&quot;,&quot;type&quot;:&quot;string&quot;,&quot;description&quot;:&quot;Default &lt;a href=\&quot;http://numeraljs.com/\&quot; target=\&quot;_blank\&quot; rel=\&quot;noopener noreferrer\&quot;&gt;numeral format&lt;/a&gt; for the \&quot;bytes\&quot; format&quot;},&quot;format:percent:defaultPattern&quot;:{&quot;name&quot;:&quot;Percent format&quot;,&quot;value&quot;:&quot;0,0.[000]%&quot;,&quot;type&quot;:&quot;string&quot;,&quot;description&quot;:&quot;Default &lt;a href=\&quot;http://numeraljs.com/\&quot; target=\&quot;_blank\&quot; rel=\&quot;noopener noreferrer\&quot;&gt;numeral format&lt;/a&gt; for the \&quot;percent\&quot; format&quot;},&quot;format:currency:defaultPattern&quot;:{&quot;name&quot;:&quot;Currency format&quot;,&quot;value&quot;:&quot;($0,0.[00])&quot;,&quot;type&quot;:&quot;string&quot;,&quot;description&quot;:&quot;Default &lt;a href=\&quot;http://numeraljs.com/\&quot; target=\&quot;_blank\&quot; rel=\&quot;noopener noreferrer\&quot;&gt;numeral format&lt;/a&gt; for the \&quot;currency\&quot; format&quot;},&quot;format:number:defaultLocale&quot;:{&quot;name&quot;:&quot;Formatting locale&quot;,&quot;value&quot;:&quot;en&quot;,&quot;type&quot;:&quot;select&quot;,&quot;options&quot;:[&quot;en&quot;,&quot;be-nl&quot;,&quot;chs&quot;,&quot;cs&quot;,&quot;da-dk&quot;,&quot;de-ch&quot;,&quot;de&quot;,&quot;en-gb&quot;,&quot;es-ES&quot;,&quot;es&quot;,&quot;et&quot;,&quot;fi&quot;,&quot;fr-CA&quot;,&quot;fr-ch&quot;,&quot;fr&quot;,&quot;hu&quot;,&quot;it&quot;,&quot;ja&quot;,&quot;nl-nl&quot;,&quot;pl&quot;,&quot;pt-br&quot;,&quot;pt-pt&quot;,&quot;ru-UA&quot;,&quot;ru&quot;,&quot;sk&quot;,&quot;th&quot;,&quot;tr&quot;,&quot;uk-UA&quot;],&quot;description&quot;:&quot;&lt;a href=\&quot;http://numeraljs.com/\&quot; target=\&quot;_blank\&quot; rel=\&quot;noopener noreferrer\&quot;&gt;Numeral language&lt;/a&gt; locale&quot;},&quot;savedObjects:perPage&quot;:{&quot;name&quot;:&quot;Objects per page&quot;,&quot;value&quot;:20,&quot;type&quot;:&quot;number&quot;,&quot;description&quot;:&quot;Number of objects to show per page in the load dialog&quot;},&quot;savedObjects:listingLimit&quot;:{&quot;name&quot;:&quot;Objects listing limit&quot;,&quot;type&quot;:&quot;number&quot;,&quot;value&quot;:1000,&quot;description&quot;:&quot;Number of objects to fetch for the listing pages&quot;},&quot;timepicker:timeDefaults&quot;:{&quot;name&quot;:&quot;Time filter defaults&quot;,&quot;value&quot;:&quot;{\n  \&quot;from\&quot;: \&quot;now-15m\&quot;,\n  \&quot;to\&quot;: \&quot;now\&quot;\n}&quot;,&quot;type&quot;:&quot;json&quot;,&quot;description&quot;:&quot;The timefilter selection to use when Kibana is started without one&quot;,&quot;requiresPageReload&quot;:true},&quot;timepicker:refreshIntervalDefaults&quot;:{&quot;name&quot;:&quot;Time filter refresh interval&quot;,&quot;value&quot;:&quot;{\n  \&quot;pause\&quot;: false,\n  \&quot;value\&quot;: 0\n}&quot;,&quot;type&quot;:&quot;json&quot;,&quot;description&quot;:&quot;The timefilter&#x27;s default refresh interval&quot;,&quot;requiresPageReload&quot;:true},&quot;timepicker:quickRanges&quot;:{&quot;name&quot;:&quot;Time filter quick ranges&quot;,&quot;value&quot;:&quot;[\n  {\n    \&quot;from\&quot;: \&quot;now/d\&quot;,\n    \&quot;to\&quot;: \&quot;now/d\&quot;,\n    \&quot;display\&quot;: \&quot;Today\&quot;\n  },\n  {\n    \&quot;from\&quot;: \&quot;now/w\&quot;,\n    \&quot;to\&quot;: \&quot;now/w\&quot;,\n    \&quot;display\&quot;: \&quot;This week\&quot;\n  },\n  {\n    \&quot;from\&quot;: \&quot;now-15m\&quot;,\n    \&quot;to\&quot;: \&quot;now\&quot;,\n    \&quot;display\&quot;: \&quot;Last 15 minutes\&quot;\n  },\n  {\n    \&quot;from\&quot;: \&quot;now-30m\&quot;,\n    \&quot;to\&quot;: \&quot;now\&quot;,\n    \&quot;display\&quot;: \&quot;Last 30 minutes\&quot;\n  },\n  {\n    \&quot;from\&quot;: \&quot;now-1h\&quot;,\n    \&quot;to\&quot;: \&quot;now\&quot;,\n    \&quot;display\&quot;: \&quot;Last 1 hour\&quot;\n  },\n  {\n    \&quot;from\&quot;: \&quot;now-24h\&quot;,\n    \&quot;to\&quot;: \&quot;now\&quot;,\n    \&quot;display\&quot;: \&quot;Last 24 hours\&quot;\n  },\n  {\n    \&quot;from\&quot;: \&quot;now-7d\&quot;,\n    \&quot;to\&quot;: \&quot;now\&quot;,\n    \&quot;display\&quot;: \&quot;Last 7 days\&quot;\n  },\n  {\n    \&quot;from\&quot;: \&quot;now-30d\&quot;,\n    \&quot;to\&quot;: \&quot;now\&quot;,\n    \&quot;display\&quot;: \&quot;Last 30 days\&quot;\n  },\n  {\n    \&quot;from\&quot;: \&quot;now-90d\&quot;,\n    \&quot;to\&quot;: \&quot;now\&quot;,\n    \&quot;display\&quot;: \&quot;Last 90 days\&quot;\n  },\n  {\n    \&quot;from\&quot;: \&quot;now-1y\&quot;,\n    \&quot;to\&quot;: \&quot;now\&quot;,\n    \&quot;display\&quot;: \&quot;Last 1 year\&quot;\n  }\n]&quot;,&quot;type&quot;:&quot;json&quot;,&quot;description&quot;:&quot;The list of ranges to show in the Quick section of the time filter. This should be an array of objects, with each object containing \&quot;from\&quot;, \&quot;to\&quot; (see &lt;a href=\&quot;https://www.elastic.co/guide/en/elasticsearch/reference/current/common-options.html#date-math\&quot;\n            target=\&quot;_blank\&quot; rel=\&quot;noopener noreferrer\&quot;&gt;accepted formats&lt;/a&gt;), and \&quot;display\&quot; (the title to be displayed).&quot;},&quot;theme:darkMode&quot;:{&quot;name&quot;:&quot;Dark mode&quot;,&quot;value&quot;:false,&quot;description&quot;:&quot;Enable a dark mode for the Kibana UI. A page refresh is required for the setting to be applied.&quot;,&quot;requiresPageReload&quot;:true},&quot;filters:pinnedByDefault&quot;:{&quot;name&quot;:&quot;Pin filters by default&quot;,&quot;value&quot;:false,&quot;description&quot;:&quot;Whether the filters should have a global state (be pinned) by default&quot;},&quot;filterEditor:suggestValues&quot;:{&quot;name&quot;:&quot;Filter editor suggest values&quot;,&quot;value&quot;:true,&quot;description&quot;:&quot;Set this property to false to prevent the filter editor from suggesting values for fields.&quot;},&quot;notifications:banner&quot;:{&quot;name&quot;:&quot;Custom banner notification&quot;,&quot;value&quot;:&quot;&quot;,&quot;type&quot;:&quot;markdown&quot;,&quot;description&quot;:&quot;A custom banner intended for temporary notices to all users. &lt;a href=\&quot;https://help.github.com/articles/basic-writing-and-formatting-syntax/\&quot;\n            target=\&quot;_blank\&quot; rel=\&quot;noopener noreferrer\&quot;&gt;Markdown supported&lt;/a&gt;.&quot;,&quot;category&quot;:[&quot;notifications&quot;]},&quot;notifications:lifetime:banner&quot;:{&quot;name&quot;:&quot;Banner notification lifetime&quot;,&quot;value&quot;:3000000,&quot;description&quot;:&quot;The time in milliseconds which a banner notification will be displayed on-screen for. Setting to Infinity will disable the countdown.&quot;,&quot;type&quot;:&quot;number&quot;,&quot;category&quot;:[&quot;notifications&quot;]},&quot;notifications:lifetime:error&quot;:{&quot;name&quot;:&quot;Error notification lifetime&quot;,&quot;value&quot;:300000,&quot;description&quot;:&quot;The time in milliseconds which an error notification will be displayed on-screen for. Setting to Infinity will disable.&quot;,&quot;type&quot;:&quot;number&quot;,&quot;category&quot;:[&quot;notifications&quot;]},&quot;notifications:lifetime:warning&quot;:{&quot;name&quot;:&quot;Warning notification lifetime&quot;,&quot;value&quot;:10000,&quot;description&quot;:&quot;The time in milliseconds which a warning notification will be displayed on-screen for. Setting to Infinity will disable.&quot;,&quot;type&quot;:&quot;number&quot;,&quot;category&quot;:[&quot;notifications&quot;]},&quot;notifications:lifetime:info&quot;:{&quot;name&quot;:&quot;Info notification lifetime&quot;,&quot;value&quot;:5000,&quot;description&quot;:&quot;The time in milliseconds which an information notification will be displayed on-screen for. Setting to Infinity will disable.&quot;,&quot;type&quot;:&quot;number&quot;,&quot;category&quot;:[&quot;notifications&quot;]},&quot;metrics:max_buckets&quot;:{&quot;name&quot;:&quot;Maximum buckets&quot;,&quot;value&quot;:2000,&quot;description&quot;:&quot;The maximum number of buckets a single datasource can return&quot;},&quot;state:storeInSessionStorage&quot;:{&quot;name&quot;:&quot;Store URLs in session storage&quot;,&quot;value&quot;:false,&quot;description&quot;:&quot;The URL can sometimes grow to be too large for some browsers to handle. To counter-act this we are testing if storing parts of the URL in session storage could help. Please let us know how it goes!&quot;},&quot;indexPattern:placeholder&quot;:{&quot;name&quot;:&quot;Index pattern placeholder&quot;,&quot;value&quot;:&quot;&quot;,&quot;description&quot;:&quot;The placeholder for the \&quot;Index pattern name\&quot; field in \&quot;Management &gt; Index Patterns &gt; Create Index Pattern\&quot;.&quot;},&quot;context:defaultSize&quot;:{&quot;name&quot;:&quot;Context size&quot;,&quot;value&quot;:5,&quot;description&quot;:&quot;The number of surrounding entries to show in the context view&quot;,&quot;category&quot;:[&quot;discover&quot;]},&quot;context:step&quot;:{&quot;name&quot;:&quot;Context size step&quot;,&quot;value&quot;:5,&quot;description&quot;:&quot;The step size to increment or decrement the context size by&quot;,&quot;category&quot;:[&quot;discover&quot;]},&quot;context:tieBreakerFields&quot;:{&quot;name&quot;:&quot;Tie breaker fields&quot;,&quot;value&quot;:[&quot;_doc&quot;],&quot;description&quot;:&quot;A comma-separated list of fields to use for tie-breaking between documents that have the same timestamp value. From this list the first field that is present and sortable in the current index pattern is used.&quot;,&quot;category&quot;:[&quot;discover&quot;]},&quot;accessibility:disableAnimations&quot;:{&quot;name&quot;:&quot;Disable Animations&quot;,&quot;value&quot;:false,&quot;description&quot;:&quot;Turn off all unnecessary animations in the Kibana UI. Refresh the page to apply the changes.&quot;,&quot;category&quot;:[&quot;accessibility&quot;],&quot;requiresPageReload&quot;:true},&quot;telemetry:optIn&quot;:{&quot;name&quot;:&quot;Telemetry opt-in&quot;,&quot;description&quot;:&quot;Help us improve the Elastic Stack by providing usage statistics for basic features. We will not share this data outside of Elastic.&quot;,&quot;value&quot;:false,&quot;readonly&quot;:true},&quot;timelion:showTutorial&quot;:{&quot;name&quot;:&quot;Show tutorial&quot;,&quot;value&quot;:false,&quot;description&quot;:&quot;Should I show the tutorial by default when entering the timelion app?&quot;,&quot;category&quot;:[&quot;timelion&quot;]},&quot;timelion:es.timefield&quot;:{&quot;name&quot;:&quot;Time field&quot;,&quot;value&quot;:&quot;@timestamp&quot;,&quot;description&quot;:&quot;Default field containing a timestamp when using .es()&quot;,&quot;category&quot;:[&quot;timelion&quot;]},&quot;timelion:es.default_index&quot;:{&quot;name&quot;:&quot;Default index&quot;,&quot;value&quot;:&quot;_all&quot;,&quot;description&quot;:&quot;Default elasticsearch index to search with .es()&quot;,&quot;category&quot;:[&quot;timelion&quot;]},&quot;timelion:target_buckets&quot;:{&quot;name&quot;:&quot;Target buckets&quot;,&quot;value&quot;:200,&quot;description&quot;:&quot;The number of buckets to shoot for when using auto intervals&quot;,&quot;category&quot;:[&quot;timelion&quot;]},&quot;timelion:max_buckets&quot;:{&quot;name&quot;:&quot;Maximum buckets&quot;,&quot;value&quot;:2000,&quot;description&quot;:&quot;The maximum number of buckets a single datasource can return&quot;,&quot;category&quot;:[&quot;timelion&quot;]},&quot;timelion:default_columns&quot;:{&quot;name&quot;:&quot;Default columns&quot;,&quot;value&quot;:2,&quot;description&quot;:&quot;Number of columns on a timelion sheet by default&quot;,&quot;category&quot;:[&quot;timelion&quot;]},&quot;timelion:default_rows&quot;:{&quot;name&quot;:&quot;Default rows&quot;,&quot;value&quot;:2,&quot;description&quot;:&quot;Number of rows on a timelion sheet by default&quot;,&quot;category&quot;:[&quot;timelion&quot;]},&quot;timelion:min_interval&quot;:{&quot;name&quot;:&quot;Minimum interval&quot;,&quot;value&quot;:&quot;1ms&quot;,&quot;description&quot;:&quot;The smallest interval that will be calculated when using \&quot;auto\&quot;&quot;,&quot;category&quot;:[&quot;timelion&quot;]},&quot;timelion:graphite.url&quot;:{&quot;name&quot;:&quot;Graphite URL&quot;,&quot;value&quot;:null,&quot;description&quot;:&quot;&lt;em&gt;[experimental]&lt;/em&gt; The &lt;a href=\&quot;https://www.hostedgraphite.com/UID/ACCESS_KEY/graphite\&quot; target=\&quot;_blank\&quot; rel=\&quot;noopener\&quot;&gt;URL&lt;/a&gt; of your graphite host&quot;,&quot;type&quot;:&quot;select&quot;,&quot;options&quot;:[],&quot;category&quot;:[&quot;timelion&quot;]},&quot;timelion:quandl.key&quot;:{&quot;name&quot;:&quot;Quandl key&quot;,&quot;value&quot;:&quot;someKeyHere&quot;,&quot;description&quot;:&quot;&lt;em&gt;[experimental]&lt;/em&gt; Your API key from www.quandl.com&quot;,&quot;category&quot;:[&quot;timelion&quot;]},&quot;xpackReporting:customPdfLogo&quot;:{&quot;name&quot;:&quot;PDF footer image&quot;,&quot;value&quot;:null,&quot;description&quot;:&quot;Custom image to use in the PDF&#x27;s footer&quot;,&quot;type&quot;:&quot;image&quot;,&quot;validation&quot;:{&quot;maxSize&quot;:{&quot;length&quot;:273066,&quot;description&quot;:&quot;200 kB&quot;}},&quot;category&quot;:[&quot;reporting&quot;]}},&quot;user&quot;:{&quot;buildNum&quot;:{&quot;userValue&quot;:29118}}}}}"></kbn-injected-metadata><div class="kibanaWelcomeView" id="kbn_loading_message" style="display:none" data-test-subj="kbnLoadingMessage"><div class="kibanaLoaderWrap"><div class="kibanaLoader"></div><div class="kibanaWelcomeLogoCircle"><div class="kibanaWelcomeLogo"></div></div></div><div class="kibanaWelcomeText" data-error-message="Kibana did not load properly. Check the server output for more information.">Loading Kibana</div></div><div class="kibanaWelcomeView" id="kbn_legacy_browser_error" style="display:none"><div class="kibanaLoaderWrap"><div class="kibanaWelcomeLogoCircle"><div class="kibanaWelcomeLogo"></div></div></div><h2 class="kibanaWelcomeTitle">Please upgrade your browser</h2><div class="kibanaWelcomeText">This Kibana installation has strict security requirements enabled that your current browser does not meet.</div></div><script>
            // Since this is an unsafe inline script, this code will not run
            // in browsers that support content security policy(CSP). This is
            // intentional as we check for the existence of __kbnCspNotEnforced__ in
            // bootstrap.
            window.__kbnCspNotEnforced__ = true;
          </script><script src="/bundles/app/kibana/bootstrap.js"></script></body></html>azadmin@ELK-SERVER:~$ 
 

Filebeat Installation

ELK Server homepage

Image: Kibana-Homepage

Open your ELK server homepage.
    - Click on **Add Log Data**.
    - Choose **System Logs**.
    - Click on the **DEB** tab under **Getting Started** to view the correct Linux Filebeat installation instructions


Create Filebeat Configuration file


Create Filebeat Installation play

Filebeat playbook

---
- name: installing and launching filebeat
  hosts: webservers
  become: yes
  tasks:
  - name: download filebeat deb
    command: curl -L -O https://artifacts.elastic.co/downloads/beats/filebeat/filebeat-7.4.0-amd64.deb
  - name: install filebeat deb
    command: dpkg -i filebeat-7.4.0-amd64.deb
  - name: drop in filebeat.yml
    copy:
      src: /etc/ansible/filebeat-config2.yml
      dest: /etc/filebeat/filebeat.yml
  - name: enable and configure system module
    command: filebeat modules enable system
  - name: setup filebeat
    command: filebeat setup --dashboards
  - name: start filebeat service
    command: service filebeat start
  - name: enable service filebeat on boot
    systemd:
      name: filebeat
      enabled: yes
  
 Command:
  
 root@7a83e6be604d:/etc/ansible# ansible-playbook filebeat-playbook.yml



Table specifying access policies and network addresses

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 10.1.0.4   | Linux            |
| Web-1    |          | 10.1.0.7   | Linux            |
| Web-2    |          | 10.1.0.8   | Linux            |
|          |          |            |                  |




A Description of Investigation you completed using Kibana




Usage Instruction





