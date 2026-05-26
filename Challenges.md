# The challenges:

## Challenge 1: The SysAdmin's "Hello, World!"

What to do:

- Set up your inventory file (hosts) by dividing your 3 machines into groups (e.g., [webservers] and [dbservers]).

- Use an Ansible ad-hoc command to ping all machines.

- Use another ad-hoc command to check disk space (df -h) but only on the [webservers] group.
<br>
Objectives: Inventory management, SSH connectivity, execution users, and ad-hoc commands.
<br><br>

## Challenge 2: Initial System Configuration (Your First Playbook)

What to do: 

- Create a playbook named system_init.yml that:

  - Updates the apt cache and upgrades all packages on the machines.

  - Installs three essential tools: curl, git, and vim.

  - Creates a new user named devops with /bin/bash as their default shell.
<br>
Objectives: Basic Playbook structure, YAML syntax, the apt and user modules, and the concept of idempotency.
<br><br>

## Challenge 3: Setting Up a Web Server (Variables and Facts)

What to do: 

- Create a playbook that:

  - Installs the Nginx web server.

  - Ensures the Nginx service is started and enabled to run at boot.

  - Replaces the default Nginx index.html using a template. This page must dynamically display the machine's IP address and hostname (using Ansible's native variables, known as Ansible Facts).
<br>
Objectives: The service/systemd modules, gathering facts (setup), and basic Jinja2 templates.
<br><br>

## Challenge 4: Automated Security (Handlers and Files)

What to do: 

- Create a security-focused playbook that:

  - Configures the firewall (ufw) to only allow traffic on ports 22 (SSH) and 80 (HTTP).

  - Copies a custom SSH configuration file (sshd_config) that disables direct root login.

  **- The catch: The SSH service should only restart if the sshd_config file actually changed.**
<br>
Objectives: The ufw module, copy or template modules, and using Handlers (notify) to trigger service restarts conditionally.
<br><br>

## Challenge 5: Clean Code with Roles

- What to do:

  - Use the command ansible-galaxy role init webserver to generate a standardized folder structure.

  - Move all the Nginx installation and configuration logic (from Challenges 3 and 4) into this Role (splitting it into tasks, templates, handlers, and vars).

  - Create a minimal main playbook that simply calls this Role for your target machines.
<br>
Objectives: Ansible directory layout, code reusability, and best practices for modular automation.
<br><br>

## Challenge 6: Protecting Sensitive Data with Ansible Vault

- What to do:

  - Create an encrypted variables file using ansible-vault. Inside, define a secure password for a new user.

  - Create a playbook that reads this encrypted file (prompting you for the vault password at execution) and uses that secret variable to create a user with that encrypted password.
<br>
Objectives: Secret management, encryption with ansible-vault, and foundational GitOps security.
<br><br>

## Challenge 7: Orchestration and Conditionals (The Ultimate Challenge)

- What to do:

  - In your inventory, define Machine 1 as the [loadbalancer] and Machines 2 and 3 as [webservers].

  - Create a single playbook using conditionals (when):

  - If the machine belongs to webservers, install Nginx with a simple webpage.

  - If the machine is the loadbalancer, install Nginx but configure it as a Reverse Proxy that routes traffic evenly to the IPs of the other two machines.
<br>
Objectives: Complex conditionals (when), loops (loop / with_items), and making an entire infrastructure talk to each other within a single execution run.
<br><br>
