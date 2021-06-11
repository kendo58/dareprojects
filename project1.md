# Project 1

SDLC is basically a process that ensures the production of quality software with minimal cost and in the fastest way (shortest production time) possible.

SDLC involves some stages:

Identify the problems to be solved
Plan the project, determining its feasibility and risks involved
Create a design plan
Build
Code Testing
And finally deployment

___
___


LAMP stack stands for Linux, Apache, Mysql and PHP. It is a set of open source software used in the development of web applications. Linux is the operating system, Apache is a web server used for hosting web applications/websites, Mysql is a relational database management system for storing application data; it stores data in tables, while PHP is a scripting language that helps build dynamic webpages.

___
___

The chmod (change mode) command is used to set permission on files and directories in Linux. The command is of the form: chmod options permissions filename FOR EXAMPLE  
__*chmod u=rxw, g=rw, o=r myfile*__

This command tells the OS to grant read, write and execute permissions to the owner of the file myfile, grant read and write to the group members of the file owner, and only read permission to other users.

The chmod command can also be written in this format: __*chmod 777 myfile*__

777 there means to grant all permissions to all users


The chown command on the other hand, lets us change ownership of a file. Command format is : chown user filename

___
___
## TCP vs UDP

TCP stands for the Transmission control protocol. It provides communication between an application program and the internet. It provides reliable and ordered delivery of data, as well as error-checking. UDP on the other hand is the User datagram protocol, which also provides communication between application on the internet. 
The main differences between these two is that UDP is connectionless whereas TCP establishes a connection between parties via a three-way handshake (SYN, ACK, SYN-ACK). TCP also guarantees data delivery while UDP is prone to data losses (reason why sometimes we see buffering when streaming videos, as most video streaming uses UDP for faster delivery, although most companies like Netflix are now moving to TCP as well). TCP also performs error checking of the data packets while UDP doesn’t.

___
___

## Some Basic Port Numbers
* Http        port  80
* Https      port 443
* Ssh        port  22
* Telnet     port 23 
* Ftp         port 21
* Sftp        port 22

___
___

# CREATING A LAMP STACK

## Installing Apache and Updating the firewall

I created an Ubuntu EC2 machine and used EC2 instance connect to connect to the EC2 instance.


* sudo apt update
* sudo apt install apache2
* sudo systemctl status apache2

to update ubuntu, install apache server and verify that the apache server is running

I viewed the web server on my webpage by using the EC2 instance's public address as my web address and the Ubuntu web server screen displayed (sorry I didn't take a screenshot at this point)
___

## Installing Mysql

* sudo apt install mysql-server
* sudo mysql_secure_installation

to install mysql and run the security script

* sudo mysql -- to log into mysql
* exit --- to exit from mysql

## Installing PHP

* sudo apt install php libapache2-mod-php php-mysql

to install all necessary packages for PHP


## Creating a virtual host for your website using Apache

* sudo mkdir /var/www/projectlamp
* sudo chown -R $USER:$USER /var/www/projectlamp
* sudo vim /etc/apache2/sites-available/projectlamp.conf

to create a new directory in the /var/www location, assign to user USER and create a new configuration file, open the file and paste in the following:

<VirtualHost *:80>
    ServerName projectlamp
    ServerAlias www.projectlamp 
    ServerAdmin webmaster@localhost
    DocumentRoot /var/www/projectlamp
    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>

then enable the new virtual host by:
* sudo a2ensite projectlamp
* sudo a2dissite 000-default
* sudo apache2ctl configtest
* sudo systemctl reload apache2

The website is now active

## Enable PHP on the website

* sudo vim /etc/apache2/mods-enabled/dir.conf
 
 and replace the content with:

 DirectoryIndex index.php index.html index.cgi index.pl index.xhtml index.htm

* sudo systemctl reload apache2
* vim /var/www/projectlamp/index.php

and add a PHP code in the vim editor

![webpage] 
(https://acbucket487384783.s3.amazonaws.com/Screen+Shot+2021-06-11+at+9.57.09+AM.png)








