# MYSQL SERVER
## Understanding
SQL is the language used to manipulate data within a relational database. With it it is possible to make all the CRUD routine necessary for a database to be useful.
There are positives and negatives to using SQL in your database, but today we're going to worry about how to just install it.

## Installation
To check if the MYSQL installation is already available in your repository, just type:

```sh
apt search mysql-server
```

If there is, the version available for installation will be returned.

To install MYSQL SERVER on your UBUNTU or derivative, just use the command below:

```sh
sudo apt update && sudo apt install mysql-server
```

Fair well, MYSQL Server is installed!

## Settings
### Password plugin
You can optionally, but **NOT** recommend **THIS**, to use a plugin for password security, to use the plugin just type:

```sh
sudo mysql_secure_installation
```

I don't recommend it at the moment because in my case I had problems with the **workbench** that we'll see later.

To start mysql type:

```sh
sudo mysql -u root -p
```

-p if you have set the password.

### User Configuration
You can create users INSIDE the mysql program using the command:

```sql
CREATE USER 'someusername'@'somelocation' IDENTIFIED by 'someusername'
```

You can change using the command:

```sql
ALTER USER 'someusername'@'somelocation' IDENTIFIED by 'someusername'
```

You can grant privileges to this user with the following commands:

```sql
GRANT ALL PRIVILEGES ON *.* TO 'someusername'@'somelocation';
FLUSH PRIVILEGES;
```

Asterisks can be changed to the names of the respective databases and tables.

Unless you know what you are doing, I really recommend using native password mode to avoid problems with Workbench.

```sql
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'typeSomePasswordHere';
```

### Uninstalling SQL
If you want to remove the SQL do:

```sh
sudo apt-get remove mysql-server mysql-client mysql-common
sudo apt-get autoremove
sudo apt-get autoclean
```

Now remove the files that were left behind:

```sh
sudo rm -rf /var/lib/mysql
sudo rm -rf /etc/mysql
```

## MYSQL WORKBENCH
This is a graphical tool that will help us to work with MYSQL.
To install it is simple, just select the OS and DISTRO you want to download and install, or follow the step by step through the official link:

> sudo rm -rf /etc/mysql

There are usually two versions.

> (mysql-workbench-community_8.0.24-1ubuntu21.04_amd64.deb)
AND
(mysql-workbench-community-dbgsym_8.0.24-1ubuntu21.04_amd64.deb)

Unless you know what you are doing, choose:
> (mysql-workbench-community_8.0.24-1ubuntu21.04_amd64.deb)
