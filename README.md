work environment for Drupal 9.1.4
included:
ubuntu:18.04
phpmyadmin:5.1.0-apache
php:7.4.15-apache
mariadb:latest

I. clone repository in root folder

git clone https://github.com/MaxChernyshev/docker.git .

II. run in project folder command: 

docker-compose up --build -d

wait a few minutes

III. open bash and enter next commands in root folder

1) make drush global

export PATH="$HOME/.composer/vendor/drush/drush:$PATH"


2) Download Drupal 9.1.4 project

composer create-project drupal/recommended-project:9.1.4 .


3) Make necessary permissions, files and folders

cp web/sites/default/default.settings.php web/sites/default/settings.php && mkdir web/sites/default/files && chmod -R 777 web/sites/default/files/ && chmod 666 web/sites/default/settings.php


4) install Drupal via Drush
drush site:install standard --db-url=mysql://root:123456@mariadb/drupal --site-name=blablabla --site-mail=blablabla@gmail.com --site-name="blablabla" --account-name=admin  --account-mail=blablabla@gmail.com --account-pass=admin -y

annotation, by default data for DB and site are shown in the command below, you should change this data with your data
//**
db name - drupal 
db user - admin 
db user password - 123456
site name - blablabla 
site mail - blablabla@gmail.com 
site name - "blablabla" 
account name - admin 
account mail - blablabla@gmail.com 
account pass - admin
**//


5) visit your in browser
site: localhost:8081/web
phpmyadmin: localhost:8080
