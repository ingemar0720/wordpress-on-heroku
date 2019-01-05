# Wordpress-on-heroku
This repository is to deploy a wordpress site on heroku service.

# Prerequisite
- install git
- apply [heroku account](https://dashboard.heroku.com/)
- apply [AWS account](https://aws.amazon.com)
- download [wordpress package](https://wordpress.org/download/)
- apply plugins and themes for wordpress(optional)

# Installation
- apply a free account on[heroku](https://dashboard.heroku.com/) and install [heroku cli](https://devcenter.heroku.com/categories/command-line)
- use heroku cli tool to login. `heroku login`
- run install.bat(Mac OS or linux please rewrite to bash script) to create app and install required plugins. Please replace `app-name` with your application name, use your `AWS_ACCESS_KEY_ID` and `AWS_SECRET_ACCESS_KEY`.
- find mysql connection information from heroku settings. 
![alt text](/img/heroku.PNG?raw=true)
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
- [add vim to heroku filesystem](https://gist.github.com/dvdbng/7375821b20f189c189ab1bd29392c98e). 
- heroku buildpack set the default maximum upload size for media to 2MB. In order to increase it, you must log in heroku bash `heroku run bash` and create [.user.ini](https://devcenter.heroku.com/articles/custom-php-settings#user-ini-files-recommended) in /app/.
- `heroku open` to open the website and install wordpress
- have fun!

# AWS S3 setup
1. log in to AWS console and find for IAM service.
1. add user 
![alt text](/img/IAM_1.PNG?raw=true)
![alt text](/img/IAM_2.PNG?raw=true)
![alt text](/img/IAM_3.PNG?raw=true)
1. retrieve 'access-key-id' and 'secret-access-key' and save it in safe place.
![alt text](/img/IAM_4.PNG?raw=true)
