# LAMP-Stack
# I- Let 's create an Apache Webserver in Linux Centos.
# 1- Installing Apache
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
# 2- Configure firewalld to Allow Apache Traffic
In a standard installation, CentOS 7 is set to prevent traffic to Apache.
Normal web traffic uses the http protocol on Port 80, while encrypted web traffic uses the https protocol, on Port 443.
# Modify your firewall to allow connections on these ports using the following commands:
```
sudo firewall-cmd ––permanent ––add-port=80/tcp
sudo firewall-cmd ––permanent ––add-port=443/tcp

```
# reload the firewall to apply the changes with the command:
```
sudo firewall-cmd --reload
```
# let check the webserver is running : 
```
ifconfig 
```
take the ip address and go to the browser
```
ip-address:80
```
# you should see a page like this: ![image](https://user-images.githubusercontent.com/85393914/165360105-b95b557b-52df-4966-baef-94728b513a51.png)

# II - Let install MariaDB 
# 1- Install the database server
```
yum install mariadb-server –y
```
# 2- Starting and enabling the database server
```
sudo systemctl start mariadb
sudo systemctl enable mariadb
```
# 3- Checking that mariadb is running
```
sudo systemctl status mariadb
```
# 4 - Let's setup the root password
```
mysql_secure_installation
```
# Follow the prompt as below
```
Enter the current password for root: Press Enter (since we don’t have one)
Set root password? : y
New password: abc123
Re enter new password: abc123
Remove anonymous users?: y
Disallow root login remotely? : y
Remove test database and access to it?:  y
Reload privilege tables now?: y
```
# 5- Accessing the database server
```
mysql -u root -p
```
# 6- show all databases
```
show databases;
```
# create bankaccount database
```
create database bankaccount;              
```
# create a user with a password
```
create user 'david'@'%' identified by 'abc123';
```
# Let's grant permissions to our new user
```
grant all privileges on bankaccount.* to 'david'@'%' identified by 'abc123';
```
# let's flush all the privileges
```
flush privileges;
```
# let's check all the privileges
```
show grants;
```
# let's create a table called todo_list within the backaccount database
```
CREATE TABLE bankaccount.todo_list ( 
item_id INT AUTO_INCREMENT, 
content VARCHAR(255), 
PRIMARY KEY(item_id) 
); 

```
```
INSERT INTO bankaccount.todo_list (content) VALUES ("My first important item"); 
```
# let's check if the table is create 
```
SELECT * FROM bankaccount.todo_list;
```
# Exit the database
```
exit
```
# III- Installing  PHP

```
yum install php php-mysql -y 
```
# Create a file called info.php in the directory /var/www/html
```
cd /var/www/html
vim info.php
```
# Add the following lines to the info.php file in the insert mode 
```
<?php
$user = “david";
$password = “abc123";
$database = “bankaccount";
$table = "todo_list";

try {
 $db = new PDO("mysql:host=localhost;dbname=$database", $user, $password);
 echo "<h2>TODO</h2><ol>"; 
 foreach($db->query("SELECT content FROM $table") as $row) {
 echo "<li>" . $row['content'] . "</li>";
 }
 echo "</ol>";
} catch (PDOException $e) {
 print "Error!: " . $e->getMessage() . "<br/>";
 die();
}
```
# Finally , go to your browser and put the ip address:80 
# you show see something like this:
![image](https://user-images.githubusercontent.com/85393914/165368610-9ee4713e-44fa-4681-a84a-212d64450256.png)













