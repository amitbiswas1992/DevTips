###   Programming Problems and Solutions

Laravel  Project Deployment in Nginx

#### Step-1 : First of all log in to your Ubutu Server

> ssh username@ip  example : ssh amit@78.325.89.90

> Step-2: cd /var/www/project_folder/html

> Then clone the project from github/gitlab

> Command : sudo git clone  https://git@gitlab.com:amit.mazegeek/Blogist.git  


#### Then go to project folder then Install and update the composer

> sudo composer install  
> sudo composer update

> Step 2.1 Permission - Example Command
> sudo chown -R amitbiswas:amitbiswas sush-website/

#### Step-3 : Open the sites-available file from nano
#### Note: make sure you are inside project domain folder  example : cd /var/www/blog.abiswas.me

> Command :   sudo nano /etc/nginx/sites-available/project
> Example :	  sudo nano /etc/nginx/sites-available/abiswas.me

#### Then edit the the file in root directory in root directory add the project path

#### Example: This line looks like this -> root /var/www/blog.abiswas.me/html;

#### You have to modify like this

> root /var/www/blog.abiswas.me/html/project_name/public;ls


#### Then add this line in location section inside { }   

 > try_files $uri $uri/ /index.php?$query_string;       
 > Reference: [Laravel](https://laravel.com/docs/5.5 "Laravel documentation")

#### Then close it and save it  and restart nginx

> Command : sudo systemctl restart nginx

#### Step-4:  give the file permission to  |   Reference: [Laravel](https://laravel.com/docs/5.5)


#### Storage and  bootstrap/cache

Command : sudo chmod -R 777 storage
sudo chmod -R 777 bootstrap/cache/

 Step-5:  generate .env file  copy .env.example file to .env
 Reference: [Laravel](https://laravel.com/docs/5.5)

>Command:  sudo cp  .env.example .env        

> then generate app  key  

> Command: sudo php artisan key:generate

> Then restart nginx

> Command:  sudo systemctl restart nginx

#### Step 6: Create database

> Go to your mysql shell  command : mysql -u root -p

> Command : CREATE DATABASE blog DEFAULT CHARACTER SET utf8 COLLATE utf8_unicode_ci;

#### Then go to your local computer terminal and export your database file in desktop

> Command: scp  database_file_name.sql  serverUaerName@ip:~

> Example: scp  blogblog_2017-09-14.sql amitbiswas@162.216.16.73:~

> Then go back to your server (nginx) terminal

> Then import the database file into the new database of your server

> Example Command: mysql -u root -p blog < blogblog_2017-09-14.sql

#### Step-7  Edit the .env file

#### Make sure you edit edit the .env file and set your database name , username  and password

#### Restart the nginx server and that's all about it . Thank you !
