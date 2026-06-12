# Oracle Linux 8 - OLVM 4.5 Installation Guide

## Environment

| Item             | Value                     |
| ---------------- | ------------------------- |
| Operating System | Oracle Linux 8.8 Minimal  |
| OLVM Version     | 4.5.5                     |
| Deployment Type  | Standalone Engine         |
| Hostname         | olvm-engine               |
| FQDN             | olvm-engine.example.local |
| IP Address       | 192.168.10.10             |

---

# 1. Configure Hostname

```bash
hostnamectl set-hostname olvm-engine
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
192.168.10.10 olvm-engine.example.local olvm-engine
EOF
```

Validate:

```bash
getent hosts olvm-engine.example.local
```

Expected result:

```text
192.168.10.10 olvm-engine.example.local olvm-engine
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
dnf config-manager --enable ol8_baseos_latest
```

Install OLVM release package:

```bash
dnf install -y oracle-ovirt-release-45-el8
```

Install UEK extra modules:

```bash
dnf install -y kernel-uek-modules-extra
```

Refresh repositories:

```bash
dnf clean all
dnf repolist
```

Expected repositories:

```text
ol8_baseos_latest
ol8_appstream
ol8_kvm_appstream
ol8_addons
ovirt-4.5
ovirt-4.5-extra
ol8_gluster_appstream
ol8_UEKR7
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

# 6. Install OLVM Engine

```bash
dnf install -y ovirt-engine
```

---

# 7. Run Engine Setup

```bash
engine-setup
```

Recommended options:

```text
Configure Cinderlib integration.................... No
Configure Engine on this host...................... Yes
Configure ovirt-provider-ovn....................... Yes
Configure WebSocket Proxy.......................... Yes
Configure Data Warehouse........................... Yes
Configure VM Console Proxy......................... Yes
Configure Grafana.................................. Yes
```

Hostname:

```text
Host fully qualified DNS name of this server....... olvm-engine.example.local
```

Database configuration:

```text
DWH Database....................................... Local
Engine Database.................................... Local
Keycloak Database.................................. Local
Configuration Mode................................. Automatic
```

Admin password:

```text
Engine admin password.............................. Use a strong password
```

Do not publish real passwords in documentation, repositories, screenshots, logs, or public issues.

Application mode:

```text
Application mode................................... Virt
```

Certificate organization:

```text
Organization name for certificate.................. Example Organization
```

Firewall:

```text
Firewall configuration............................. Automatic
```

Data Warehouse sampling scale:

```text
Data Warehouse sampling scale...................... Basic
```

Confirm installation:

```text
Please confirm installation settings............... Ok
```

Installation may take several minutes.

---

# 8. Validate Engine Services

```bash
systemctl status ovirt-engine
systemctl status ovirt-engine-dwhd
systemctl status grafana-server
```

Restart Engine if required:

```bash
systemctl restart ovirt-engine
```

---

# 9. Access OLVM Portal

Administration Portal:

```text
https://olvm-engine.example.local/ovirt-engine
```

Keycloak Administration:

```text
https://olvm-engine.example.local/ovirt-engine-auth/admin
```

Grafana:

```text
https://olvm-engine.example.local/ovirt-engine-grafana
```

Default login:

```text
Username: admin@ovirt
Password: <password-defined-during-engine-setup>
```

---

# 10. Prepare Local Storage

# Create base storage structure
mkdir -p /home/vmstorage/{vms,iso,templates,backups,exports}

# Assign ownership for OLVM/KVM
chown -R vdsm:kvm /home/vmstorage

# Set permissions
chmod -R 0755 /home/vmstorage

# Validate
ls -ld /home/vmstorage
ls -lh /home/vmstorage

---

# Installation Completed

The OLVM Engine is now ready for:

* Datacenter creation
* Cluster creation
* Host onboarding
* Storage Domain creation
* Virtual Machine deployment

---

## References

Oracle Linux Virtualization Manager Documentation:

https://docs.oracle.com/en/virtualization/oracle-linux-virtualization-manager/
