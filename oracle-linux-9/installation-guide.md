Segue o bloco ajustado para `oracle-linux-9/installation-guide.md`, com dados genéricos e sem senha real.

# Oracle Linux 9 - OLVM 4.5 Installation Guide

## Environment

| Item                 | Value                     |
| -------------------- | ------------------------- |
| Operating System     | Oracle Linux 9 Minimal    |
| OLVM Version         | 4.5.5                     |
| Deployment Type      | Self-Hosted Engine        |
| Base Hostname        | olvm-host                 |
| Base Host FQDN       | olvm-host.example.local   |
| Base Host IP Address | 192.168.10.11             |
| Engine VM Hostname   | olvm-engine               |
| Engine VM FQDN       | olvm-engine.example.local |
| Engine VM IP Address | 192.168.10.12             |

---

# 1. Configure Hostname

```bash
hostnamectl set-hostname olvm-host
```

Validate:

```bash
hostnamectl
hostname -f
```

---

# 2. Configure Hosts File

```bash
cat << 'EOF' >> /etc/hosts
192.168.10.11 olvm-host.example.local olvm-host
192.168.10.12 olvm-engine.example.local olvm-engine
EOF
```

Validate:

```bash
getent hosts olvm-host.example.local
getent hosts olvm-engine.example.local
```

Expected result:

```text
192.168.10.11 olvm-host.example.local olvm-host
192.168.10.12 olvm-engine.example.local olvm-engine
```

---

# 3. Update Operating System

```bash
dnf update -y
reboot
```

---

# 4. Enable Required Repositories

```bash
dnf config-manager --enable ol9_baseos_latest
```

Install OLVM release package:

```bash
dnf install -y oracle-ovirt-release-45-el9
```

Refresh repositories:

```bash
dnf clean all
dnf repolist
```

Expected repositories:

```text
ol9_baseos_latest
ol9_appstream
ol9_kvm_appstream
ol9_addons
ol9_kvm_utils
ovirt-4.5
ovirt-4.5-extra
ol9_UEKR8
```

---

# 5. Run OLVM Pre-Check

```bash
olvm-pre-check.py
```

Expected result:

```text
PASS
```

Possible warning:

```text
The FQDN is coming from the system /etc/hosts file.
It is recommended to use an external DNS Server for Name Resolution.
```

This warning is expected when DNS is not configured and name resolution is provided through `/etc/hosts`.

For production environments, external DNS resolution is recommended.

---

# 6. Install Hosted Engine Packages

```bash
dnf install -y ovirt-hosted-engine-setup ovirt-engine-appliance
```

---

# 7. Deploy Self-Hosted Engine

```bash
hosted-engine --deploy --4
```

Recommended options:

```text
Are you sure you want to continue?.................. Yes
NIC for ovirtmgmt bridge........................... ens192
Network connectivity check......................... ping
Data center........................................ Default
Cluster............................................ Default
Configure Keycloak integration..................... No
```

Appliance configuration:

```text
Appliance image path............................... <press Enter>
Engine VM vCPUs.................................... 4
Engine VM memory................................... 4096
Engine VM FQDN..................................... olvm-engine.example.local
Engine VM domain................................... example.local
```

Root access:

```text
Root password for engine appliance................. Use a strong password
SSH public key..................................... Optional
Enable SSH access for root......................... yes
```

Security options:

```text
Apply OpenSCAP security profile.................... No
Enable FIPS........................................ No
```

Network configuration:

```text
Engine VM MAC address.............................. <press Enter>
Engine VM network configuration.................... Static
Engine VM IP address............................... 192.168.10.12
Engine VM DNS...................................... <your DNS server>
Add lines to /etc/hosts............................ Yes
```

SMTP notification configuration:

```text
SMTP server........................................ Optional
SMTP port.......................................... Optional
Notification sender............................... Optional
Notification recipients........................... Optional
```

Engine credentials:

```text
Engine admin password.............................. Use a strong password
```

Do not publish real passwords in documentation, repositories, screenshots, logs, or public issues.

Management host:

```text
Hostname of this host on the management network.... olvm-host.example.local
```

Confirm the deployment and wait for the process to complete.

---

# 8. Validate Hosted Engine Status

```bash
hosted-engine --vm-status
```

Validate services:

```bash
systemctl status ovirt-ha-agent
systemctl status ovirt-ha-broker
```

---

# 9. Access OLVM Portal

Administration Portal:

```text
https://olvm-engine.example.local/ovirt-engine
```

Default login:

```text
Username: admin@ovirt
Password: <password-defined-during-hosted-engine-deployment>
```

---

# 10. Post-Installation Validation

Validate:

```bash
hosted-engine --vm-status
```

Check that:

* Hosted Engine VM is running
* HA Agent is active
* HA Broker is active
* OLVM Web Administration Portal is accessible
* Base host appears in the OLVM Administration Portal
* Datacenter is available
* Cluster is available

---

# 11. Prepare Local Storage

## Create base storage structure
```text
mkdir -p /home/vmstorage/{vms,iso,templates,backups,exports}
```

## Assign ownership for OLVM/KVM
```text
chown -R vdsm:kvm /home/vmstorage
```

## Set permissions
```text
chmod -R 0755 /home/vmstorage
```

## Validate
```text
ls -ld /home/vmstorage
ls -lh /home/vmstorage
```

# Installation Completed

The OLVM Self-Hosted Engine deployment is now ready for:

* Datacenter validation
* Cluster validation
* Host management
* Storage Domain creation
* Network configuration
* Virtual Machine deployment

---

## References

Oracle Linux Virtualization Manager Documentation:

[https://docs.oracle.com/en/virtualization/oracle-linux-virtualization-manager/](https://docs.oracle.com/en/virtualization/oracle-linux-virtualization-manager/)
