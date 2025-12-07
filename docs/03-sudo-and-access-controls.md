# 03 – Sudo and Access Controls

This section demonstrates least-privilege administration using sudo.

## Verifying Default Sudo Access

The system uses the wheel group for sudo access.

Verification:

grep wheel /etc/sudoers  
id student  

## Granting Sudo Access to taylor

The devops user taylor was added to the wheel group:

usermod -aG wheel taylor  
id taylor  

This allows taylor to use sudo without giving full root access directly.

## Creating a Restricted Sudo Policy

A custom sudo policy file was created:

visudo -f /etc/sudoers.d/devops  

The following rule was added:

taylor ALL=(ALL) NOPASSWD: /usr/bin/systemctl restart httpd, /usr/bin/systemctl status httpd, /usr/bin/journalctl -u httpd

This limits taylor to only web service control and log review.

## Validating Sudo Configuration

Syntax validation:

visudo -c  

## Testing Sudo Restrictions

As taylor:

sudo systemctl status httpd  
sudo systemctl restart httpd  
sudo journalctl -u httpd  

Unauthorized test:

sudo dnf update  

This correctly required a password or denied access, proving least-privilege enforcement.

