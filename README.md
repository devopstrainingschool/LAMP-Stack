# LAMP-Stack
I- Let 's create an Apache Webserver in Linux Centos.
1- Installing Apache
# Downoad and install Apache
```
sudo yum update -y
sudo yum install httpd -y 
```
# Start and enable httpd
```
sudo systemctl start httpd 
sudo systemctl enable httpd
```
# verify that Apache is running
```
sudo systemctl status httpd
```
2- Configure firewalld to Allow Apache Traffic
In a standard installation, CentOS 7 is set to prevent traffic to Apache.
Normal web traffic uses the http protocol on Port 80, while encrypted web traffic uses the https protocol, on Port 443.
# Modify your firewall to allow connections on these ports using the following commands:
```
sudo firewall-cmd ––permanent ––add-port=80/tcp
sudo firewall-cmd ––permanent ––add-port=443/tcp

```
# reload the firewall to apply the changes with the command:
```
sudo firewall-cmd -- reload
```

