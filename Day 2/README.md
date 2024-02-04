The directory structure separates roles, variables, and configurations.
Variables like packages and sites are defined in role defaults or vars for better organization.
Handlers are used for tasks that require notification triggers.
Templates (httpd.conf.j2, nginx.conf.j2 and auth.conf.j2) can be populated based on your specific Apache configuration and authentication needs.

Run the playbook:

```
ansible-playbook install_web_servers.yml -e @web_servers_variables.yml
```

Project Description: Web Infrastructure Automation with Ansible

This project aims to automate the setup and configuration of a web infrastructure using Ansible, a powerful open-source automation tool. The infrastructure consists of backend servers running Apache (httpd) and a load balancer server running Nginx. Additionally, PHP-related packages are installed on servers with total memory greater than 1GB.

### Project Components:

1. **Ansible Playbooks:**

   - **`install_web_servers.yml`:** The main Ansible playbook orchestrating the installation and configuration of web servers.
   - **`web_servers_variables.yml`:** Variables file containing host information, such as IP addresses and domain names.

2. **Roles:**

   - **`common`:**

     - Installs common packages like EPEL repository and the firewall service based on the OS family.
     - Installs PHP-related packages on servers with total memory larger than 1GB.

   - **`webserver`:**

     - Installs and configures Apache (httpd) on backend servers.
     - Configures virtual hosts and Apache authentication for specified sites.

   - **`loadbalancer`:**
     - Installs and configures Nginx on the load balancer server.
     - Configures Nginx to proxy traffic to backend servers.

3. **Files:**

   - **`inventory.ini`:** Defines host groups for backend and load balancer servers.
   - **`ansible.cfg`:** Ansible configuration file specifying roles path and inventory file location.
   - **`web_servers_variables.yml`:** Host and variable information for the playbook.

4. **Templates:**

   - **`roles/webserver/templates/httpd.conf.j2`:** Apache (httpd) configuration template.
   - **`roles/webserver/templates/auth.conf.j2`:** Apache authentication configuration template.
   - **`roles/loadbalancer/templates/nginx.conf.j2`:** Nginx configuration template.

5. **Handlers:**
   - Reloads the firewall service after changes are made to firewall settings.

### Execution Steps:

1. Run the main playbook (`install_web_servers.yml`).
2. Ansible installs common packages, sets up the firewall, and installs PHP-related packages based on memory size.
3. Backend servers are configured with Apache, and the load balancer server is configured with Nginx.
4. Apache is configured with virtual hosts and authentication for specified sites.

### Note:

- Adjust variables and configurations in the playbook, roles, and templates according to specific project requirements.
- This project structure follows best practices for Ansible organization, modularization, and variable management.
- Regularly update variables, configuration templates, and tasks to adapt to evolving project needs.

This project provides a foundation for automating the deployment and maintenance of web infrastructure, ensuring consistency and efficiency in managing servers.
