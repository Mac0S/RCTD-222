Environment
----
1. Instal Apache
```
yum install httpd httpd-devel
```
2. Install MySQL or MariaDB
```
# 喜歡老妹的選這個
yum install mysql mysql-server
# 喜歡嫩妹的選這個
yum install mariadb-server -y
```
3. Install PHP
```
yum install php-mysql php-pear php-common php-gd php-devel php php-mbstring php-cli
```
4. Install PHP-SNMP
```
yum install php-snmp
```
5. Install NET-SNMP
```
yum install net-snmp-utils net-snmp-libs
```
6. Install RRDTool
```
yum install rrdtool
```
Starting Services
----
```
# For CentOS 6.x/5.x
[root@tecmint ~]# service httpd start
[root@tecmint ~]# service mysqld start
[root@tecmint ~]# service snmpd starty

# For CentOS 7.x
[root@tecmint ~]# systemctl start httpd.service
[root@tecmint ~]# systemctl start mariadb.service
[root@tecmint ~]# systemctl start snmpd.service
```
Configure System Start-up Links
---
```
# For CentOS 6.x/5.x
[root@tecmint ~]# /sbin/chkconfig --levels 345 httpd on
[root@tecmint ~]# /sbin/chkconfig --levels 345 mysqld on
[root@tecmint ~]# /sbin/chkconfig --levels 345 snmpd on

# For CentOS 7.x
[root@tecmint ~]# systemctl enable httpd.service
[root@tecmint ~]# systemctl enable mariadb.service
[root@tecmint ~]# systemctl enable snmpd.service
```
Install Cacti
---
Install Cacti By Auto
```
# Best Choise for lazy.
yum install cacti
```
Install Cacti By Manual
```
# Best Choise for 假掰.
wget https://www.cacti.net/downloads/幹，版本自己選好嗎


# tar and mv folder to web folder
tar cacti
mv cacti /var/www/html/cacti
cd /var/www/html

# Setting the privileged
chown -R apache:apache cacti
chown root:apache /var/lib/php/sessions
```
Configuring MySQL Server for cacti installation
```
# Initial MariaDB (Press Y for all)
mysql_secure_installation

# Create Cacti Database from MySQL
mysql -u root -p
create database cacti;
GRANT ALL ON cacti.* TO cacti@localhost IDENTIFIED BY 'cactiuser';
FLUSH privileges;
quit;

# find cacti.sql location (1 for auto install, 2 for manual isntall)
rpm -ql cacti | grep cacti.sql
or
/var/www/html/cacti/cacti.sql

# input cacti.sql to database
mysql -u cacti -p cacti < /xxx/xxx/cacti.sql


# configure Cacti setting for connect to MySQL
/* make sure these values reflect your actual database/host/user/password */
$database_type = "mysql";
$database_default = "cacti";
$database_hostname = "localhost";
$database_username = "cacti";
$database_password = "your-password-here";
$database_port = "3306";
$database_ssl = false;
```
Configuring Firewall for Cacti
---
```
# On RHEL/CentOS 6.x/5.x
[root@tecmint ~]# iptables -A INPUT -p udp -m state --state NEW --dport 80 -j ACCEPT
[root@tecmint ~]# iptables -A INPUT -p tcp -m state --state NEW --dport 80 -j ACCEPT
[root@tecmint ~]# service iptables save

# On RHEL/CentOS 7.x
[root@tecmint ~]# firewall-cmd --permanent --zone=public --add-service=http
[root@tecmint ~]# firewall-cmd --reload
```
Configuring Apache Server for Cacti Installation
---
```
test

```