# mysql

## Docker & kubernetes
```
$ docker run mysql  -e MYSQL_ROOT_PASSWORD=123 -e MYSQL_ALLOW_EMPTY_PASSWORD=no -e MYSQL_RANDOM_ROOT_PASSWORD=no

$ kubectl run mysql --image=mysql --env=MYSQL_ROOT_PASSWORD=123 --env=MYSQL_ALLOW_EMPTY_PASSWORD=no --env=MYSQL_RANDOM_ROOT_PASSWORD=no
```

## Install mysql mariadb

* https://blog.microlinux.fr/mysql-centos-7/

```bash
for file in $(rpm -qa|grep mysql); do yum erase -y $file; done
rm /var/lib/mysql/*  -fr
yum install mariadb-server mariadb
systemctl enable mariadb --now
systemctl start mariadb

### Secure mysql installation
mysql_secure_installation

mysql -u root -p
show databases;
use mysql;
select User,Host,Password from user;
delete from user where host!='localhost';
```

### Create an user
```
CREATE USER 'newuserlogin'@'localhost' IDENTIFIED  BY 'ItAFakePasswd';
GRANT ALL PRIVILEGES ON *.* TO 'newuserlogin'@'localhost';
```
### Show ACL Access
```bash
show grants for 'root'@'localhost';
```

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
