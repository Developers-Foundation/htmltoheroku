# Hosting HTML apps on Heroku
This mini-tutorial will guide you through the process of hosting your HTML webiste on Heroku for free. 

## Deploy a Website with Heroku
[Heroku](https://www.heroku.com/) is a platform for managing cloud-based apps. It allows you to deploy and test your web app easily without having to worry about managing servers. 

### Set up Heroku
Start by creating a [Heroku Account](https://toolbelt.heroku.com/).

Since we're only interested in a simple HTML website, we'll be using PHP as our server-side language. We first need to install a few things.

#### 1. Install [PHP](http://php.net/)
You only do this once to your computer. 

#### 2. Get [Composer](https://getcomposer.org/download/)
Composer is a dependency manager for PHP. We will need it to obtain the Heroku dependencies for our project. 
You can download and install composer from the terminal by running the following commands:

```
php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
php -r "if (hash_file('SHA384', 'composer-setup.php') === 'aa96f26c2b67226a324c27919f1eb05f21c248b987e6195cad9690d5c1ff713d53020a02ac8c217dbf90a7eacc9d141d') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"
php composer-setup.php
php -r "unlink('composer-setup.php');"
```

This will generate a composer.phar file which you will be able to use in any PHP project to install dependencies. 

</br>
NOTE: If the commands above do not work, then go to the website itself to download the latest version. 

#### 3. Obtain the [Heroku Toolbelt](https://toolbelt.heroku.com/)
This will help you manage and deploy Heroku Apps.
Once downloaded, you can enter your Heroku credentials via the following command in your terminal:

```
$ heroku login
```

You are now ready to create your first Heroku App.

### Create Heroku App 

#### Setup
Create a folder where your Heroku project will reside. Create another folder (web) inside myapp, which will contain the actual code for your website (your HTML and CSS files):

```
$ mkdir myapp
$ cd myapp
$ mkdir web
```

Create a file called **composer.json** and populate it with the following code:

```json
{
  "require-dev" : {
   "heroku/heroku-buildpack-php": "*"
  }
}
```

This file is what Composer uses to download the dependencies. 
In order to download the dependancies, copy the composer.phar file we generated earlier to this **myapp folder** and run the following command:

```
$ php composer.phar install
```

After the dependancies are created, create an index.php file in the **web folder**, populate it with the following code:

```PHP
<?php include_once("index.html");?>
```

All this script does is tell the server to load the index.html file when someone accesses the website. Create an index.html file in the same 'web' folder. 
The following is just an example, you will use your own code when populating your own index.html

```html
<!DOCTYPE html>
<html lang="en">
<head>
   <meta charset="UTF-8">
   <title>Random title</title>
</head>
<body>
   <p>Hello World!</p>
</body>
</html>
```

Finally, before we can deploy on Heroku, we need to create one more file called Procfile in the main **myapp folder**.
Put the following line in a file called Procfile:

```
web: vendor/bin/heroku-php-apache2 web/
```

When your app is deployed on Heroku, this file tells the server how to run your app. In this case, it uses an apache server to run whatever is inside the web folder.


##Final Structure
    -> [myapp]
        -> [vendor]
            -> [bin]
            -> [composer]
            -> [heroku/heroku-buildpack]
            -autoload.pho
        -> [web]
            -> YOUR WEBSITE (HTML, CSS & JS)
        -> Procfile
        -> composer.json
        -> composer.loc
        -> composer.phar
        
 Note: [] remembles folder names.
        
#### Adjust your directory
Make sure your terminal directory is in the right place. 

#### Deploy!
You are finally ready to deploy your project. 

Initialize a git repository:

```
$ git init
$ git add . && git commit -m "Initial Commit"
```

use the following command to link to a Heroku Remote:

```
$ heroku create
```

Deploy your project by pushing to the Heroku remote:

```
$ git push heroku master
```

View your project in a browser!

```
$ heroku open
```





