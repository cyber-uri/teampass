# How to install TeamPass on Ubuntu 22.04

## Prerequisites

Before installing Teampass, ensure the following:
  - You have a Ubuntu Server installed
  - You have a sudo user account

## Update System
    
It is always a good practice to update the system before installing any new software.

```bash
  sudo apt update && sudo apt upgrade
```
## Install LAMP Stack

Teampass requires LAMP stack to be installed on the server. To do that, run the following command:

```bash
  sudo apt-get install apache2 php mysql-server php-mysql libapache2-mod-php php-xml php-mbstring
```

## Download Teampass

Download the teampass directory on GitHub with ```git clone```:

```bash
  git clone http://github.com/nilsteampassnet/TeamPass
```
Move directory to /var/www/html:

```bash
  sudo mv TeamPass/ /var/www/html
```

Change the ownership of the Teampass directory:

```bash
  sudo chown -R www-data:www-data /var/www/html/TeamPass
```

We can ensure that we have changed the owner correctly with the following command:

```bash
  ls -l /var/www/html
  total 16
  -rw-r--r--  1 root     root     10671 ago 23 07:13 index.html
  drwxrwxr-x 17 www-data www-data  4096 ago 23 07:26 TeamPass
  uri@uri:~$ 

```

## Crete MySQL Database and User

Teampass requires a MySQL database and a user to access it. To create it, run the following commands: 

```bash
  sudo mysql -u root -p
```

You will be prompted to enter the root user password. After that, create a new database:

```bash
  CREATE DATABASE teampassdb;
```

Now create a new databasee user with the username and password of your choice:

```bash
  CREATE USER 'teampassuser'@'localhost' IDENTIFIED BY 'p4$$w0rd01';
```

Grant this user all privileges on the teampassdb database:

```bash
  GRANT ALL PRIVILEGES ON teampassdb.* TO 'teampassuser'@'localhost' WITH GRANT OPTION;
```

Flush the privileges and exit the MySQL shell:


```bash
  FLUSH PRIVILEGES;
  exit;
```
## Configure Teampass

Copy the configuration file:

```bash
  sudo cp /var/www/html/TeamPass/includes/config/settings.sample.php /var/www/html/TeamPass/includes/config/config.php
```

Open the new configuration file:

```bash
  sudo nano /var/www/html/teampass/includes/config/teampass.config.php
```

Change the database details to match the database:

```bash
  define("DB_HOST", "localhost");
  define("DB_USER", "teampassuser");
  define("DB_PASSWD", "p4$$w0rd01");
  define("DB_NAME", "teampassdb");
  define("DB_PREFIX", "");
  define("DB_PORT", "3306");
  define("DB_ENCODING", "utf8");
```
Make sure to save the changes.

## Enable Apache rewrite Module

Teampass uses Apache's mod_rewrite module to display the correct URLs. To enable it, run the following command:

```bash
  sudo systemctl restart apache2
  sudo a2enmod rewrite
  sudo systemctl restart apache2
```

## Acces Teampass

Open a web browser and go to http://your-server-ip/TeamPass/ to access a Teampass Install.
