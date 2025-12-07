# 01 – Environment Setup

## Host and Guest Overview

- Host OS: macOS
- Virtualization: VMware Fusion
- Guest OS: Red Hat Enterprise Linux (RHEL) 9/10
- VM name: rhel10-lab.local
- Primary user: student (sudo-enabled)

## Initial Verification Commands

After the first login, I verified the OS and kernel:

cat /etc/redhat-release
uname -r
hostnamectl

I also confirmed basic networking:

ip a
ping -c 2 google.com

## System Updates and Base Tools

I updated the system and installed base tools used throughout the lab:

sudo dnf -y update
sudo dnf -y install vim tree git lvm2

- vim – text editor  
- tree – directory visualization  
- git – version control client  
- lvm2 – logical volume management tools  

## Security Baseline – Default State

Before hardening, I captured the default state of key services:

sudo systemctl status firewalld
sudo systemctl status sshd

Enabled services at boot:

systemctl list-unit-files --type=service | grep enabled | head -20

This established a baseline before applying any security changes later in the lab.

