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

  


# The challenges:

## Challenge 1: The SysAdmin's "Hello, World!"

What to do:

- Set up your inventory file (hosts) by dividing your 3 machines into groups (e.g., [webservers] and [dbservers]).

- Use an Ansible ad-hoc command to ping all machines.

- Use another ad-hoc command to check disk space (df -h) but only on the [webservers] group.


Objectives: Inventory management, SSH connectivity, execution users, and ad-hoc commands.


## Challenge 2: Initial System Configuration (Your First Playbook)

What to do: 

- Create a playbook named system_init.yml that:

  - Updates the apt cache and upgrades all packages on the machines.

  - Installs three essential tools: curl, git, and vim.

  - Creates a new user named devops with /bin/bash as their default shell.

Objectives: Basic Playbook structure, YAML syntax, the apt and user modules, and the concept of idempotency.


Challenge 3: Setting Up a Web Server (Variables and Facts)

What to do: 

- Create a playbook that:

  - Installs the Nginx web server.

  - Ensures the Nginx service is started and enabled to run at boot.

  - Replaces the default Nginx index.html using a template. This page must dynamically display the machine's IP address and hostname (using Ansible's native variables, known as Ansible Facts).

Objectives: The service/systemd modules, gathering facts (setup), and basic Jinja2 templates.


Challenge 4: Automated Security (Handlers and Files)

What to do: 

- Create a security-focused playbook that:

  - Configures the firewall (ufw) to only allow traffic on ports 22 (SSH) and 80 (HTTP).

  - Copies a custom SSH configuration file (sshd_config) that disables direct root login.

  **- The catch: The SSH service should only restart if the sshd_config file actually changed.**

Objectives: The ufw module, copy or template modules, and using Handlers (notify) to trigger service restarts conditionally.


Challenge 5: Clean Code with Roles

- What to do:

  - Use the command ansible-galaxy role init webserver to generate a standardized folder structure.

  - Move all the Nginx installation and configuration logic (from Challenges 3 and 4) into this Role (splitting it into tasks, templates, handlers, and vars).

  - Create a minimal main playbook that simply calls this Role for your target machines.

Objectives: Ansible directory layout, code reusability, and best practices for modular automation.


Challenge 6: Protecting Sensitive Data with Ansible Vault

- What to do:

  - Create an encrypted variables file using ansible-vault. Inside, define a secure password for a new user.

  - Create a playbook that reads this encrypted file (prompting you for the vault password at execution) and uses that secret variable to create a user with that encrypted password.

Objectives: Secret management, encryption with ansible-vault, and foundational GitOps security.


Challenge 7: Orchestration and Conditionals (The Ultimate Challenge)

- What to do:

  - In your inventory, define Machine 1 as the [loadbalancer] and Machines 2 and 3 as [webservers].

  - Create a single playbook using conditionals (when):

  - If the machine belongs to webservers, install Nginx with a simple webpage.

  - If the machine is the loadbalancer, install Nginx but configure it as a Reverse Proxy that routes traffic evenly to the IPs of the other two machines.

Objectives: Complex conditionals (when), loops (loop / with_items), and making an entire infrastructure talk to each other within a single execution run.
