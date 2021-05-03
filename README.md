# ELK
ELK-Project

1.Activities for Azure setup and ELK Server configuration

A. Create a Resource Group on Azure
B. Create a new Virtual Network
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

    Then click on Create

    ....Initializing Deployment to 
    ....Your deployment is complete
    
    
    Image: Image1-VirtualNetwork-ELK-NET
    
C.  Create peer connection to allow traffic pass between virtual networks and regions

	Navigate to 'Virtual Network' in the Azure Portal.
	Select your new vNet to view it's details.
	Under 'Settings' on the left side, select 'Peerings'.
	Click the + Add button to create a new Peering.
    
    Image: Image2-Elk-Peering
    
    
 D. 


  
  








Table specifying access policies and network addresses




A Description of Investigation you completed using Kibana




Usage Instruction





