# Nginx Load Balancer and Web Servers Setup

This project is designed to set up a **Load Balancer** with Nginx and several web servers using **Ansible**. One of the web servers will act as a load balancer, distributing incoming traffic between two backend web servers. Each web server will serve a simple landing page that displays the correct IP address of the respective server.

## Project Structure

The project directory structure is as follows:


### Key Files:

- **`inventory/hosts.yml`**: Contains the IP addresses of all web servers and the load balancer.
- **`nginx_playbook.yml`**: The main Ansible playbook to set up Nginx and configure the load balancer.
- **`nginx/tasks/main.yml`**: Defines the tasks for installing Nginx, configuring the load balancer, and creating landing pages.
- **`nginx/templates/load_balancer.conf.j2`**: The template for the Nginx configuration file for the load balancer.
- **`nginx/vars/main.yml`**: Defines the variables, including the content of the landing pages for web servers.

## Prerequisites

Before running the playbook, ensure you have the following:

- **Ansible** installed and configured on your local machine or control node.
- **Python** installed on the target servers.
- **SSH access** to the target servers.
- **Virtual Machines (VMs) or Physical Servers** running with valid IP addresses.

## Configuration

### 1. Modify the Inventory File

The **`inventory/hosts.yml`** file contains the IP addresses of the web servers and the load balancer. You will need to replace the placeholder IPs with the actual IPs of your servers.

Example:

```yaml
all:
  children:
    webservers:
      hosts:
        webserver1:
          ansible_host: 192.168.56.112  # IP of your first web server
        webserver2:
          ansible_host: 192.168.56.113  # IP of your second web server
        webserver3:
          ansible_host: 192.168.56.111  # IP of your load balancer (this should be a web server too)

nginx_web_server_content: |
  <h1>Welcome to WebServer type {{ ansible_hostname }} with IP {{ ansible_host }}</h1>


