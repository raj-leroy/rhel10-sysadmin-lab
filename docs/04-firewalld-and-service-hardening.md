# 04 – firewalld and Service Hardening

This section demonstrates host-based firewall configuration and basic service attack-surface reduction.

## Enabling and Verifying firewalld

The firewall service was enabled and started:

sudo systemctl enable --now firewalld  
sudo systemctl status firewalld  

Active firewall zones:

sudo firewall-cmd --get-active-zones  

Current active rules:

sudo firewall-cmd --list-all  

## Locking Down Network Access

By default, only SSH should be allowed.

Allow SSH permanently:

sudo firewall-cmd --permanent --add-service=ssh  

Reload rules:

sudo firewall-cmd --reload  
sudo firewall-cmd --list-all  

If Apache is running, HTTP was explicitly allowed:

sudo firewall-cmd --permanent --add-service=http  
sudo firewall-cmd --reload  
sudo firewall-cmd --list-all  

This confirms that only explicitly authorized services are exposed.

## SSH Hardening

The SSH configuration file was backed up and updated:

sudo cp /etc/ssh/sshd_config /etc/ssh/sshd_config.bak  
sudo vim /etc/ssh/sshd_config  

The following values were verified or enforced:

PermitRootLogin no  
PasswordAuthentication yes  
PubkeyAuthentication yes  

SSH service was restarted:

sudo systemctl restart sshd  
sudo systemctl status sshd  

## Service Attack-Surface Reduction

Enabled services were reviewed:

systemctl list-unit-files --type=service | grep enabled | head -20  

An unnecessary service was disabled (example below):

sudo systemctl disable --now cups.service  

This reduces the overall attack surface of the system.

