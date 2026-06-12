# OLVM Installation Guide

Practical documentation for installing and configuring Oracle Linux Virtualization Manager (OLVM).

This repository provides step-by-step installation guides for deploying OLVM on Oracle Linux environments.

## Installation Guides

* [Oracle Linux 8 - OLVM 4.5 Installation Guide](oracle-linux-8/installation-guide.md)
* [Oracle Linux 9 - OLVM 4.5 Installation Guide](oracle-linux-9/installation-guide.md)

## Validation Checklist

Before considering the OLVM deployment complete, validate:

* [ ] Oracle Linux updated successfully
* [ ] Hostname configured correctly
* [ ] FQDN resolving correctly
* [ ] Required repositories enabled
* [ ] `olvm-pre-check.py` executed successfully
* [ ] OLVM Engine installed
* [ ] `engine-setup` completed without errors
* [ ] Engine service running
* [ ] Web Administration Portal accessible
* [ ] Keycloak accessible
* [ ] Grafana accessible
* [ ] Data Warehouse running
* [ ] Firewall rules configured
* [ ] Storage directories created
* [ ] Storage permissions validated
* [ ] Datacenter created
* [ ] Cluster created
* [ ] Host added successfully
* [ ] Storage Domain active
* [ ] Test VM created successfully

## Supported Versions

| Oracle Linux   | OLVM Version | Status      |
| -------------- | ------------ | ----------- |
| Oracle Linux 8 | OLVM 4.5     | Supported   |
| Oracle Linux 9 | OLVM 4.5     | In Progress |

## Features Covered

* Oracle Linux preparation
* Repository configuration
* OLVM package installation
* Engine deployment
* Data Warehouse configuration
* Grafana integration
* Keycloak integration
* Storage preparation
* Host onboarding
* Datacenter configuration
* Cluster configuration
* Troubleshooting

## Deployment Type

This repository focuses on:

* Standalone Engine Deployment
* KVM Virtualization
* Local Storage
* Laboratory and Production Environments

## Official Documentation

Oracle Linux Virtualization Manager:

https://docs.oracle.com/en/virtualization/oracle-linux-virtualization-manager/

## Disclaimer

The procedures documented in this repository were validated in laboratory environments.

Always validate installation and upgrade procedures before applying them to production environments.
