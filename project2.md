# Project 2



# CREATING A LEMP STACK

## Installing the Nginx web server

I created an Ubuntu EC2 machine and used EC2 instance connect to connect to the EC2 instance.


* sudo apt update
* sudo apt install nginx
* sudo systemctl status nginx

to update ubuntu, install nginx server and verify that the server is running

I viewed the web server on my webpage by using the EC2 instance's public address as my web address and the Nginx web server screen displayed 
___

## Installing Mysql

* sudo apt install mysql-server
* sudo mysql_secure_installation

to install mysql and run the security script

* sudo mysql -- to log into mysql
* exit --- to exit from mysql

## Installing PHP

* sudo apt install php-fpm php-mysql

to install all necessary packages for PHP


## Configuring Nginx to use PHP Processor

* sudo mkdir /var/www/projectlemp
* sudo chown -R $USER:$USER /var/www/projectlemp
* sudo nano /etc/nginx/sites-available/projectlemp.conf

to create a new directory in the /var/www location, assign to user USER and create a new configuration file, open the file and paste in the following:

#/etc/nginx/sites-available/projectLEMP

server {
    listen 80;
    server_name projectLEMP www.projectLEMP;
    root /var/www/projectLEMP;

    index index.html index.htm index.php;

    location / {
        try_files $uri $uri/ =404;
    }

    location ~ \.php$ {
        include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/var/run/php/php7.4-fpm.sock;
     }

    location ~ /\.ht {
        deny all;
    }

}

to activate the configuration:
* sudo ln -s /etc/nginx/sites-available/projectLEMP /etc/nginx/sites-enabled/

then: 
* sudo nginx -t
* sudo unlink /etc/nginx/sites-enabled/default
* sudo echo 'Hello LEMP from hostname' $(curl -s http://169.254.169.254/latest/meta-data/public-hostname) 'with public IP' $(curl -s http://169.254.169.254/latest/meta-data/public-ipv4) > /var/www/projectLEMP/index.html

The website is now active

## Test PHP

* sudo nano /var/www/projectLEMP/info.php
 
* <?php
phpinfo();


## Retrieving Data from Mysql Database

* sudo mysql
* CREATE DATABASE `example_database`;
* CREATE USER 'ekene'@'%' IDENTIFIED WITH mysql_native_password BY 'kenny';
* GRANT ALL ON example_database.* TO 'ekene'@'%';
* exit
* mysql -u example_user -p
* SHOW DATABASES;

to create a table:

CREATE TABLE example_database.todo_list (
item_id INT AUTO_INCREMENT,
content VARCHAR(255),
PRIMARY KEY(item_id)
);

insert into table:
* INSERT INTO example_database.todo_list (content) VALUES ("My first important item");

* SELECT * FROM example_database.todo_list;

exit and then :

* nano /var/www/projectLEMP/todo_list.php

paste in the PHP script to connect to mysql database

![webpage]
(https://acbucket487384783.s3.amazonaws.com/Screen+Shot+2021-06-12+at+7.17.20+AM.png)

![webpabe]
(https://acbucket487384783.s3.amazonaws.com/Screen+Shot+2021-06-12+at+7.30.29+AM.png)

(https://acbucket487384783.s3.amazonaws.com/Screen+Shot+2021-06-12+at+7.43.18+AM.png)

(https://acbucket487384783.s3.amazonaws.com/Screen+Shot+2021-06-12+at+7.45.43+AM.png)







