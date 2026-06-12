# OLVM Installation Guide

Practical documentation for installing and configuring Oracle Linux Virtualization Manager (OLVM).

This repository provides step-by-step installation guides for deploying OLVM 4.5 on Oracle Linux environments using both Standalone Engine and Self-Hosted Engine architectures.

The goal is to provide a practical and reproducible installation reference, complementing Oracle's official documentation with real-world deployment examples.

## Installation Guides

### Oracle Linux 8

**Deployment Type:** Standalone Engine

* [Oracle Linux 8 - OLVM 4.5 Installation Guide](oracle-linux-8/installation-guide.md)

### Oracle Linux 9

**Deployment Type:** Self-Hosted Engine

* [Oracle Linux 9 - OLVM 4.5 Installation Guide](oracle-linux-9/installation-guide.md)

---

## Supported Versions

| Oracle Linux   | OLVM Version | Deployment Type    | Status    |
| -------------- | ------------ | ------------------ | --------- |
| Oracle Linux 8 | 4.5.5        | Standalone Engine  | Supported |
| Oracle Linux 9 | 4.5.5        | Self-Hosted Engine | Supported |

---

## Validation Checklist

Before considering the OLVM deployment complete, validate:

### Operating System

* [ ] Oracle Linux updated successfully
* [ ] Hostname configured correctly
* [ ] FQDN resolving correctly
* [ ] Required repositories enabled
* [ ] `olvm-pre-check.py` executed successfully

### OLVM Installation

* [ ] OLVM packages installed successfully
* [ ] Deployment completed without errors
* [ ] Engine services running
* [ ] Web Administration Portal accessible

### Infrastructure

* [ ] Datacenter created
* [ ] Cluster created
* [ ] Host added successfully
* [ ] Storage Domain active
* [ ] Network configuration validated

### Validation Tests

* [ ] Test virtual machine created
* [ ] VM startup validated
* [ ] VM console access validated
* [ ] Storage operations validated

### Self-Hosted Engine (Oracle Linux 9)

* [ ] Hosted Engine VM running
* [ ] HA Agent active
* [ ] HA Broker active
* [ ] Hosted Engine status healthy

---

## Features Covered

* Oracle Linux preparation
* Repository configuration
* OLVM package installation
* Standalone Engine deployment
* Self-Hosted Engine deployment
* Keycloak integration
* Grafana integration
* Data Warehouse configuration
* Storage preparation
* Datacenter configuration
* Cluster configuration
* Host onboarding
* Virtual machine provisioning
* Troubleshooting and validation procedures

---

## Repository Structure

```text
.
├── README.md
│
├── oracle-linux-8
│   └── installation-guide.md
│
├── oracle-linux-9
│   └── installation-guide.md
│
├── images
│
└── LICENSE
```

---

## Official Documentation

Oracle Linux Virtualization Manager Documentation:

https://docs.oracle.com/en/virtualization/oracle-linux-virtualization-manager/

Oracle Linux Documentation:

https://docs.oracle.com/en/operating-systems/oracle-linux/

---

## Disclaimer

The procedures documented in this repository were validated in laboratory environments.

Always validate installation, upgrades, migrations, and configuration changes in a non-production environment before applying them to critical workloads.

Oracle®, Oracle Linux®, KVM®, and Oracle Linux Virtualization Manager® are trademarks of their respective owners.
