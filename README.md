# mysql

### Install mysql repo

```bash
yum localinstall https://dev.mysql.com/get/mysql57-community-release-el7-11.noarch.rpm
yum install mysql-community-server
```

### Basics queries

```bash
show databases;

 USE `database`;
 SHOW TABLES;

 SHOW TABLES FROM `database`;
 
 show fields  from table;
 show columns from table;
 ```
 
## Flush root password

```bash
#
systemctl stop mysql
mysqld_safe --skip-grant-tables &
mysql -u root
use mysql;
update user set authentication_string=PASSWORD("mynewpassword") where User='root';
flush privileges;
quit
systemctl stop mysql
systemctl start mysql
```
