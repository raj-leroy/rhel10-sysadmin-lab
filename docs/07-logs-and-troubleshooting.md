# 07 – Logs and Incident Troubleshooting

This section demonstrates detection and investigation of authentication failures and service errors using journald.

## Simulating Failed SSH Login Attempts

Multiple failed SSH logins were generated:

ssh student@localhost  

Incorrect passwords were entered multiple times to simulate a brute-force pattern.

## Reviewing Authentication Logs

Security logs were reviewed using traditional and journald methods:

sudo tail -n 20 /var/log/secure  

sudo journalctl -u sshd --since "15 minutes ago"  

Filtered failed login attempts:

sudo journalctl -u sshd | grep "Failed password"  

This confirmed visibility into authentication attack attempts.

## Simulating a Service Failure (httpd)

A controlled failure was introduced into the Apache configuration:

sudo cp /etc/httpd/conf/httpd.conf /etc/httpd/conf/httpd.conf.bak  
echo "BROKEN_DIRECTIVE" | sudo tee -a /etc/httpd/conf/httpd.conf  
sudo systemctl restart httpd  

The service failed as expected.

## Root Cause Analysis Using Journald

Service failure was investigated:

sudo systemctl status httpd  
sudo journalctl -u httpd --since "10 minutes ago"  

The logs clearly identified a configuration syntax failure.

## Service Recovery

The original configuration was restored:

sudo mv /etc/httpd/conf/httpd.conf.bak /etc/httpd/conf/httpd.conf  
sudo systemctl restart httpd  
sudo systemctl status httpd  

This confirmed successful incident recovery and service restoration.

