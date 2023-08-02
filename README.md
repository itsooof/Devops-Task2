# Devops-Task2
Ansible Playbook: Deploy Node Exporter, Prometheus, and Grafana

This Ansible playbook is designed to deploy Node Exporter, Prometheus, and Grafana on a local machine. Node Exporter is a Prometheus exporter that collects system metrics from the machine. Prometheus is a monitoring and alerting toolkit, and Grafana is used for data visualization.
Prerequisites

Before running this playbook, ensure that the following requirements are met:

    Ansible is installed on your local machine.
    The target machine is reachable and properly configured for Ansible communication.
    Make sure that the prometheus.yml.j2 and grafana_datasource.yml files are present in the same directory as this playbook.

How to Use

    Clone this repository to your local machine.
    Navigate to the directory containing the playbook and template files.
    Review the playbook to make sure the tasks and configurations suit your specific use case and environment.
    Run the playbook using the following command:

bash

ansible-playbook playbook.yml

Replace playbook.yml with the name of the file containing the Ansible code.
Playbook Overview

The playbook consists of the following tasks:

    Install necessary dependencies (curl) using the apt package manager if it is available.
    Download Node Exporter from GitHub using get_url and store it in /tmp/node_exporter.tar.gz.
    Extract the Node Exporter archive to /tmp using unarchive.
    Copy the Node Exporter binary to /usr/local/bin/node_exporter with appropriate permissions (0755).
    Create a system user named node_exporter.
    Set up a systemd service for Node Exporter with the provided configuration.
    Create a Prometheus config file using a template prometheus.yml.j2 and place it in /etc/prometheus/prometheus.yml.
    Create a Grafana provisioning file named grafana_datasource.yml and store it in /etc/grafana/provisioning/datasources/prometheus.yml.

Additionally, there are handlers defined to reload systemd, Prometheus, and Grafana after any configuration changes are made.
Configuration Files

Make sure the following configuration files are present in the playbook directory:

    prometheus.yml.j2: Template for Prometheus configuration file.
    grafana_datasource.yml: Configuration file for Grafana provisioning.

Please customize these files according to your monitoring and visualization needs.
Notes

    This playbook is intended for deployment on a local machine. For production environments, additional considerations and security measures should be taken.

    Please ensure you have the necessary permissions to execute this playbook and modify system configurations on the target machine.

    If you encounter any issues or errors during the deployment, review the playbook, configurations, and the target machine's setup to resolve the problems.

    For more information about Ansible and its capabilities, refer to the official Ansible documentation.
