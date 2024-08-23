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
