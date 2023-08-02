# Ansible Playbook to Deploy Node Exporter on Multiple Hosts and Set Up Grafana & Prometheus

## Step 1: Prerequisites

Before proceeding with the playbook, ensure that you have the following prerequisites:

    Ansible installed on your laptop.
    Multiple target hosts where you want to deploy Node Exporter (ensure SSH access is set up).

## Step 2: Create the Ansible Playbook

Create a new file named deploy_node_exporter.yml with the following content:

yaml

---
- name: Deploy Node Exporter
  hosts: your_target_group  # Replace with the group of hosts defined in your hosts file

  tasks:
    - name: Install Node Exporter
      apt:
        name: prometheus-node-exporter  # For Ubuntu/Debian systems. Adjust package name for other systems.
        state: present
      become: true

    # Add any other tasks you need for the deployment
    # For example, you might want to start the Node Exporter service and enable it to start on boot.

Replace your_target_group with the appropriate group name from your hosts file. If you don't have an existing hosts file, create one and define your target hosts:

ini

[your_target_group]
hostname1
hostname2
hostname3
# Add all your target hosts here

## Step 3: Deploy Node Exporter to Multiple Hosts

Run the Ansible playbook using the following command:

bash

ansible-playbook -i /path/to/your/hosts/file deploy_node_exporter.yml

This will install Node Exporter on all the target hosts specified in the your_target_group.

## Step 4: Set Up Grafana & Prometheus on Your Laptop

Follow these steps to set up Grafana and Prometheus on your laptop:

    Install Grafana:
        Download and install Grafana from the official website: https://grafana.com/grafana/download
        Start the Grafana server using the appropriate command for your operating system.

    Install Prometheus:

        Download and install Prometheus from the official website: https://prometheus.io/download

        Extract the downloaded archive and navigate to the Prometheus directory.

        Modify the prometheus.yml configuration file to scrape data from Node Exporter on your target hosts. For example:

        yaml

        global:
          scrape_interval: 15s

        scrape_configs:
          - job_name: 'node_exporter'
            static_configs:
              - targets: ['hostname1:9100', 'hostname2:9100', 'hostname3:9100']

        Replace hostname1, hostname2, etc., with the actual hostnames or IP addresses of your target hosts.

        Start Prometheus using the appropriate command for your operating system.

    Configure Grafana Data Source:
        Open Grafana in your web browser (http://localhost:3000 by default).
        Log in with the default credentials (admin/admin).
        Add a Prometheus data source:
            Click on the "Configuration" gear icon on the left sidebar.
            Select "Data Sources" and click on "Add data source."
            Choose "Prometheus" as the data source type.
            Configure the URL to point to your locally running Prometheus instance (e.g., http://localhost:9090).
            Save the data source.

    Create Grafana Dashboards:
        Explore Grafana's dashboard panel and create visualizations using the data from Prometheus.
        Import pre-built dashboards for Node Exporter metrics from the Grafana dashboard repository or create your custom dashboards.

## Step 5: Monitor Node Exporter Metrics

Now that you have set up Grafana and Prometheus on your laptop, you can monitor the metrics collected from Node Exporter on your target hosts. Grafana will display the visualizations based on the data fetched from Prometheus.
