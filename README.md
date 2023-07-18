☁️ Nextcloud ☁️
===================

This Ansible playbook is created to install and preconfigure Nextcloud on a Debian system without having to use the WebGUI.

It consists out of 5 roles:

1️⃣ **Install**				    ----- This will install packages like apache2 & mysql-server & php dependencies

2️⃣ **Download**				  ----- This downloads the latest Nextcloud installer and unpacks it

3️⃣ **Database**				  ----- This configures the mysql-server, adds a user and privileges

4️⃣ **Apacheconfig**			----- This configures Apache2 and enables the Nextcloud webpage

5️⃣ **Postinstall**				----- This initializes the database and configures Nextcloud using occ

---

Each role has a few tasks:

1️⃣ **Install**

1. Installs apache2, mysql-server, php, zip , libapache2-mod-php , php-gd, php-json , php-mysql, php-curl , php-mbstring, php-intl , php-imagick , php-xml, php-zip , php-mysql , php-bcmath , php-gmp , pip
2. Create a Nextcloud cache directory for the installer download from https://download.nextcloud.com/server/releases/

2️⃣ **Download**

1. Download the latest Nextcloud installer to the cache directory (latest.tar.bz2)
2. Create the Nextcloud www-root directory
3. Unpack the tar file to the www-root directory
4. Give /var/www/html/nextcloud perms

3️⃣ **Database**

1. Makes sure pip is upgraded to be able to install PyMysql
2. Install pip PyMysql package
3. Create the "NEXTCLOUD" database in Mysql
4. Create database user ""NEXTCLOUD_USER"" for database "NEXTCLOUD"

4️⃣ **Apacheconfig**

1. Configure Apache vhost "NEXTCLOUD"
2. Check whether site "NEXTCLOUD" is already enabled
3. a2enmod en restart apache
4. Reload apache2

5️⃣ **Postinstall**

1. Give perms to nextcloud dir for db initialisation
2. Initialise the database and config.php (only works for fresh Nextcloud installation) using the occ command.
3. Insert the trusted ip domain in the config file at /var/www/html/nextcloud/nextcloud/config/config.php


⚙️ Variables ⚙️
===================

These variables can be customized for your own system and are found in the main directory in the playbook file: **nextcloud.yml**

| var            | default value                               | description                                                                 |
| -------------- | ------------------------------------------- | --------------------------------------------------------------------------- |
| nc_directory   | /var/www/html/nextcloud                     | This is the directory where the Nextcloud webpage files will be stores      |
| nc_cache       | nc_cache                                    | This is the directory where the Nextcloud installer will download to        |
| a2_se          | /etc/apache2/sites-enabled/nextcloud.conf   | This is the path to the nextcloud.conf file in sites-enabled                |
| a2_sa          | /etc/apache2/sites-available/NEXTCLOUD.conf | This is the path to the NEXTCLOUD.conf file in sites-available              |
| db_name        | NEXTCLOUD                                   | This is the database name                                                   |
| db_login       | root                                        | This is the database login                                                  |
| db_sock        | /var/run/mysqld/mysqld.sock                 | This is where the MySql socket is                                           |
| db_pw          | test123                                     | This is the password for the created database                               |
| nc_user        | NEXTCLOUD_USER                              | This is the username for the Nextcloud application                          |
| nc_pw          | test123                                     | This is the password for the Nextcloud application                          |
| trusted_domain | 192.168.1.124                               | This is the domain were the webpage is hosted on, added as a trusted domain |

⭐ Usage ⭐
===========

Customize the variables in **nextcloud.yml** and run the playbook with ansible-playbook nextcloud.yml


🧙🏻‍♂️ Author Information 🧙🏻‍♂️
========================================

333sky
