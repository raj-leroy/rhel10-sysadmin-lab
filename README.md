# RHEL System Administration and Security Hardening Lab

This project documents a complete hands-on Linux system administration and security hardening lab using Red Hat Enterprise Linux in a virtualized environment. The goal of this lab was to build real-world foundational experience with enterprise Linux administration, access control, firewall management, service operations, storage configuration, and security log analysis.

This repository serves as technical proof of my Linux, systems, and security fundamentals for entry-level IT, system administration, and cybersecurity roles.

---

## Environment Overview

Host System:
- macOS
- VMware Fusion

Guest System:
- Red Hat Enterprise Linux (RHEL)
- Hostname: `rhel10-lab.local`
- Primary User: `student` (sudo-enabled)

---

## Core Skills Demonstrated

- Linux system installation and patch management
- Local user and group identity management
- POSIX permissions and shared directory access controls
- Least-privilege sudo policy enforcement
- firewalld host-based firewall configuration
- SSH service hardening
- systemd service installation, enablement, and monitoring
- Apache (httpd) deployment and operational management
- Enterprise storage configuration using LVM
- Persistent filesystem mounting with `/etc/fstab`
- Security log analysis using journald and `/var/log/secure`
- Incident investigation and service recovery

---

## Lab Breakdown

Each section below is fully documented with commands, validation steps, and outcomes.

### 01 – Environment Setup
- Verified OS, kernel, hostname, and networking
- Applied full system updates using dnf
- Installed base administrative tools
- Captured firewall and SSH baseline state

File:
- `docs/01-environment-setup.md`

---

### 02 – Users, Groups, and Permissions
- Created dev and ops groups
- Created users and assigned group membership
- Built a shared project directory at `/srv/projects`
- Enforced group-based write permissions using setgid
- Validated access enforcement with permission denial testing

File:
- `docs/02-users-groups-permissions.md`

---

### 03 – Sudo and Access Controls
- Verified default sudo configuration
- Implemented least-privilege sudo policy for DevOps-style user
- Restricted privileged actions to specific systemctl and journalctl commands
- Verified denial of unauthorized privileged operations

File:
- `docs/03-sudo-and-access-controls.md`

---

### 04 – firewalld and Service Hardening
- Enabled and configured firewalld
- Restricted exposed services to SSH and HTTP only
- Hardened SSH by disabling root login
- Audited enabled services and reduced attack surface

File:
- `docs/04-firewalld-and-service-hardening.md`

---

### 05 – Patching and Service Management
- Verified system update status
- Applied full patch upgrades
- Installed and deployed Apache (httpd)
- Validated service availability using curl
- Performed service restarts and log validation via journald

File:
- `docs/05-patching-and-service-management.md`

---

### 06 – Storage and LVM
- Added a secondary virtual disk
- Created physical volume, volume group, and logical volume
- Formatted XFS filesystem
- Mounted logical volume at `/data`
- Configured persistent mounting using `/etc/fstab`

File:
- `docs/06-storage-and-lvm.md`

---

### 07 – Logs and Incident Troubleshooting
- Simulated failed SSH authentication attempts
- Investigated authentication failures using journald and secure logs
- Introduced controlled Apache service failure
- Performed root cause analysis using systemctl and journalctl
- Restored service operation and verified recovery

File:
- `docs/07-logs-and-troubleshooting.md`

---

## Validation Screenshots

Live verification screenshots for each major lab section are stored in the `screenshots/` directory:

1. RHEL version and hostname  
2. Users, groups, and permission enforcement  
3. Least-privilege sudo policy validation  
4. firewalld and SSH hardening  
5. Apache service management and logs  
6. LVM storage mounted at `/data`  
7. Journald incident detection and recovery  

---

## Purpose of This Lab

This project was built to:
- Develop hands-on Linux system administration skill
- Practice security baseline configuration
- Demonstrate operational troubleshooting and incident response
- Provide transparent technical proof for recruiters and hiring managers

All actions were executed manually in a live RHEL virtual machine and documented step-by-step.

---

## Author

Rajiv Leroy  
Entry-Level Linux System Administration & Cybersecurity  
Columbia, SC
