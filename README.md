Proxmox Monitoring Deployment with Ansible

This repository automates the deployment of Grafana and InfluxDB on a container for monitoring Proxmox server vitals.
Prerequisites

Ansible installed on your local machine.
SSH access to the target container.
A valid SSH private key for authentication.

Setup

Clone the repository:

    git clone https://github.com/luisbaronceli/Install-Grafana-and-Influx-DB-for-Proxmox-monitoring.git
    cd proxmox-monitoring-ansible/ansible

Update Inventory:

Edit the inventory/hosts file to include the IP address or hostname of your target container.

    [servers]
    your_server_ip_or_hostname ansible_user=root

Configure SSH Key:

Ensure the ansible.cfg file has the correct path to your SSH private key.

    [defaults]
    inventory = inventory/hosts
    remote_user = root
    
    [ssh_connection]
    private_key_file = /path/to/your/private/key

Running the Playbook

Run the Ansible playbook to deploy Grafana and InfluxDB:

    ansible-playbook playbook.yml --private-key=/path/to/your/private/key

Post-Deployment

After running the playbook, Grafana and InfluxDB should be installed and running on your container. Access Grafana via its web interface on port 3000.
InfluxDB Configuration

The InfluxDB configuration template is located at roles/influxdb/templates/influxdb.conf.j2. Modify this template to suit your specific needs (e.g., changing the database name).
Proxmox Setup

Set up a metrics server in Proxmox by navigating to Datacenter > Metric Server > add. Ensure the server name matches the database name (default: proxmox).
Setting up Grafana

Access Grafana on port 3000 and set a new Data source:
    Go to Configuration > Data Sources > Add Data Source.
    Search for InfluxDB, then click on Add new datasource.
    Configure:
        HTTP URL: http://<your-server-ip>:8086
        InfluxDB Details-Database: proxmox (or your specified database name)
    Save & Test.

Import a dashboard:
    Home > Dashboards > Import Dashboard.
    Copy the JSON from this repository or any other suitable dashboard.
    Click Import and load the JSON.
    Edit dashboard settings (e.g., Variables) to match the database source.
    If widgets are not displaying correctly, edit each widget and change the data source to proxmox.

Additional Information

This repository automates tasks demonstrated in this YouTube video from a different person: (https://www.youtube.com/watch?v=LRXq3TFW-tk&t=165s). 
Watching the video might be useful to troubleshoot any issues or if you have any difficulties with the promox Metrics Server or the Grafana dashboard set up.

