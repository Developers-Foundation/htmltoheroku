# Hosting HTML apps on Heroku
This mini-tutorial will guide you through the process of hosting your HTML webiste on Heroku for free. 

## Deploy a Website with Heroku
[Heroku](https://www.heroku.com/) is a platform for managing cloud-based apps. It allows you to deploy and test your web app easily without having to worry about managing servers. 

### Set up Heroku
Start by creating a [Heroku Account](https://toolbelt.heroku.com/).

Since we're only interested in a simple HTML website, we'll be using PHP as our server-side language. We first need to install a few things.

#### 0. Setup the accounts required

- Heorku
- Github
- Optional but preferably JetBrains using their PHPStorm as the IDE via this [link](https://www.jetbrains.com/shop/eform/students)

#### 0.5 Install Git (Only required on Windows)

1. (Download it here)[https://git-scm.com/download/win]
2. Run it
3. Open the Git Bash (now should be installed)

#### 1. Install [PHP](http://php.net/)
You only do this once to your computer.

##### Mac

0. If HomeBrew is not installed yet run `/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"`
1. In the App Store install the newest version of XCode.
2. On your terminal run:

```
brew update
brew tap homebrew/dupes
brew tap homebrew/versions
brew tap homebrew/homebrew-php
brew unlink php56
brew install php70
pico /etc/paths
```

3. Make sure `/usr/local/bin` is above all other lines in that file, if not then move it there
4. Click Control+X -> Y -> Enter Key to quit the editor
5. Quit and restart terminal

##### Windows
Good luck :P Message Harrison to walk you through this.

1. Download php from [here](http://windows.php.net/download) (I suggest sticking with 7.0 builds for now, and go with thread-safe, since you won't be doing much heavy compiling)
2. Unzip the content from into C://php/ (You will have to make the folder if you haven't installed before). If you want to enable multi-ver builds, use this structure: C://php/php56 and C://php/php70
3. Change the file name of php.ini-developement or php.ini-stable into php.ini
4. Setup environment variable in control panel (You can find this by searching it)
5. Start Git Bash and try `php -v`, if it says `Command not found.`, run `echo $PATH` and make sure `C:/php/` is in the list. If not add it by using `export PATH=$PATH:C/php` (Note: I don't have pc, so setting this might be diff)

#### 2. Get [Composer](https://getcomposer.org/download/)
Composer is a dependency manager for PHP. We will need it to obtain the Heroku dependencies for our project. 
Install composer for the local project by:

1. Visit [getcomposer.org](http://getcomposer.org/download/) and download the latest `composer.phar`
2. Move it into the root of your project folder (the top folder of your git repo)
3. Run `php composer.phar init`
4. Follow the instructions on terminal (If not required, you can have most fields blank)
5. Add the following line into the composer.json, check the sample composer.json file for where to add this:

```
"require-dev" : {
   "heroku/heroku-buildpack-php": "*"
  }
```

6. Check the remaining things inside the `composer.json` is correct then run `php composer.phar update`


#### 3. Optional: Obtain the [Heroku Toolbelt](https://toolbelt.heroku.com/)
This will help you manage and deploy Heroku Apps.
Once downloaded, you can enter your Heroku credentials via the following command in your terminal:

```
heroku login
```

You are now ready to create your first Heroku App.

#### 4. Upload to GitHub then Heroku

1. Log into GitHub and make a new repository using the green button. Name it what you want, and don't add readme, or any other files
2. Click create then copy out the link of the repository
3. On your GitBash and inside the directory (use `cd folderName` to navigate to the root of the folder, run `git init`
4. Run the following commands:

```
git remote add origin pasteInTheURLHere
git add .
git commit -m "hello world :P"
git push -u origin master
```

5. The folder is now setup, and you should see your files in GitHub
6. Setup the Heroku website by making a new app on Heroku. Just fill in the form to your liking, and once done, visit the deploy section. Click GitHub for the source of the code, connect your GitHub account, and search the repository name under the field. Then click enable automatic deploy.
7. Click Deploy Branch to create the first website. If something goes wrong at this step, good idea to contact Harrison (Everything is case by case, and you may have hit a bug in above steps)
8. Click view to see your first website 

#### AND YOU ARE DONE :P

## FOLLOWING STEPS BELOW IS DEPRECATED.

##### Create Heroku App 

##### Setup
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





