# ansible
****************
3 Ubuntu machines, 1 Master &amp; 2 Subs, being managed by using Ansible playbooks
****************

This project was made with the objective of improving the knowledge with:
- VMWare (Virtualization)
- Ubuntu (Configuration & Administration)
- Ansible (Automation)

****************

The project starts with creating and configuring 3 VMs, all of them with Ubuntu Server 26.04.
These 3 VMs were created in order to serve the porpose of one "Control Node" (CD) and the other 2 as "Managed Nodes" (MN).

<img width="534" height="270" alt="image" src="https://github.com/user-attachments/assets/e475ad85-992d-4618-ab2d-fec1c8f2a90e" />

# Enable SSH on both MNs, and edit user permissions.

## Enabling SSH
sudo apt update # To update all available packages

sudo apt install ssh # To install the package needed for SSH

sudo ufw allow 22 # To open the port 22, if not done already

## Edit user permissions for SSH
sudo visudo # To open the file where sudo users are configured

YOUR_USER ALL=(ALL) NOPASSWD:ALL # Add this at the end of the file

# Set up a list of Hosts for the CN to use, so, we will create the following structure and file (if its not already there)

<img width="114" height="36" alt="image" src="https://github.com/user-attachments/assets/e2f5b037-9bc4-4e7a-85be-962175b82eb7" />

## On the 'hosts' file, we will first create a group using [GROUP_NAME], using the structure:

  [GROUP_NAME]
  
  server1 ansible_host=IP_ADDRESS
  
  server2 ansible_host=IP_ADDRESS
  

## And below, another section will be added in order to specify the ssh credentials to be used. In my case, i have the same user on both machines.

  [GROUP_NAME:vars]
  
  ansible_user=USER_NAME
  
  ansible_password=USER_PASSWORD

  
