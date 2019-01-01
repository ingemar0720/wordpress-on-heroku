# Wordpress-on-heroku
This repository is to deploy a wordpress site on heroku service.

# Prerequisite
1. install git
1. apply [heroku account](https://dashboard.heroku.com/)
1. apply [AWS account](https://aws.amazon.com)
1. download [wordpress package](https://wordpress.org/download/)
1. apply plugins and themes for wordpress(optional)

# Installation
- apply a free account on[heroku](https://dashboard.heroku.com/) and install [heroku cli](https://devcenter.heroku.com/categories/command-line)
- use heroku cli tool to login. `heroku login`
- run install.bat(Mac OS or linux please rewrite to bash script) to create app and install required plugins. Please replace `app-name` with your application name, use your `AWS_ACCESS_KEY_ID` and `AWS_SECRET_ACCESS_KEY`.
- find mysql connection information from heroku settings. 
![alt text](http://url/to/heroku.png)
JAWSDB URL format is mysql://`DB_USER`:`DB_PASSWORD`@`DB_HOST`/`DB_NAME`
- apply a [aws account](https://aws.amazon.com)and follow the guide to create new IAM user and access policy for S3.
- unzip wordpress package, copy `wp-config-sample.php` to `wp-config.php`, amend the content and map JAWSDB information into the file.
- fill in S3 access-key-id and secret-access-key into wp-config.php
```
define( 'AS3CF_SETTINGS', serialize( array(
    'provider' => 'aws',
    'access-key-id' => 'ACCESS-KEY-ID',
    'secret-access-key' => 'SECRET-ACCESS-KEY',
) ) );
```
- type `git init`, `git add .`, `git commit -am "first commit"`, `heroku git:remote -a app-name` and `git push heroku master` to upload and deploy the wordpress to heroku.
- heroku buildpack set the default maximum upload size for media to 2MB. In order to increase it, you must log in heroku bash `heroku run bash` and create [.user.ini](https://devcenter.heroku.com/articles/custom-php-settings#user-ini-files-recommended) in /app/.
- `heroku open` to open the website and install wordpress
- have fun!

# AWS S3 setup
1. log in to AWS console and find for IAM service.
1. add user 
![create user](http://url/to/IAM_1.png)
![alt text](http://url/to/IAM_2.png)
![alt text](http://url/to/IAM_3.png)
1. retrieve 'access-key-id' and 'secret-access-key' and save it in safe place.
![alt text](http://url/to/IAM_4.png)
