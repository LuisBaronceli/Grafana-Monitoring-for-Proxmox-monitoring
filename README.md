# Proxmox Monitoring Deployment with Ansible

This repository contains Ansible playbooks and roles to automate the deployment of Grafana and InfluxDB on a container. These tools are used to monitor the vitals of a Proxmox server.

## Prerequisites

- Ansible installed on your local machine.
- SSH access to the target container where Grafana and InfluxDB will be installed.
- A valid SSH private key for authentication.

## Setup

1. **Clone the repository:**
   
   git clone https://github.com/luisbaronceli/Install-Grafana-and-Influx-DB-for-Proxmox-monitoring.git
   cd proxmox-monitoring-ansible/ansible


2. **Update Inventory:**
Edit the inventory/hosts file to include the IP address or hostname of your target container.

  [servers]
  your_server_ip_or_hostname ansible_user=root

3. **Configure SSH Key:**
Ensure the ansible.cfg file has the correct path to your SSH private key.

    [defaults]
    inventory = inventory/hosts
    remote_user = root

    [ssh_connection]
    private_key_file = /path/to/your/private/key

4. **Running the Playbook**

  Run the Ansible playbook to deploy Grafana and InfluxDB:
  ansible-playbook playbook.yml --private-key=/path/to/your/private/key

