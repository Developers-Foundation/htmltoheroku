# Hosting HTML apps on Heroku
This mini-tutorial will guide you through the process of hosting your HTML webiste on Heroku for free. 

[Heroku](https://www.heroku.com/) is a platform for managing cloud-based apps. It allows you to deploy and test your web app easily without having to worry about managing servers. 

## 0. Setup the accounts required

- [Heroku](https://www.heroku.com/)
- [Github](https://github.com/)

## 1. Install Git

### Linux
```
sudo apt-get install git
```

### Windows
Download and run the installer from [here](https://git-scm.com/download/win).
Once you've completed the isntallation, a program called Git Bash will be installed on your system. This is a Linux-like terminal for windows and you will be using this terminal for the rest of the guide.

### macOS
Just try to run `git` from the terminal. If you dont already have it installed, it will prompt you to install it.

## 2. Upload your code to GitHub

1. After logging into GitHub, create a new repository using the green button. 
2. Name it what you want, and don't add readme, or any other files
2. Click create then copy the URL of your repository (you will need it in the first command below)
3. In your terminal, [navigate](https://www.digitalocean.com/community/tutorials/basic-linux-navigation-and-file-management) to the root folder of your website
4. Initialize your repo: `git init`
5. Add Github as a remote (make sure to add the URL you copied earlier): `git remote add origin REPLACE_WITH_REPO_URL`
6. Now run the following commands to add, commit and push your code to Github:
```
git add .
git commit -m "initial commit"
git push -u origin master
```
Now go back to your Github page and open the repository you just created (make sure to refresh). All your code should be there

## 3. Prepare your app to be deployed

All these steps are done in the root directory:
1. Rename your index.html (or whatever you named your homepage) to home.html
2. Create a file called index.php with this code inside: `<?php include_once("home.html"); ?>`
3. Create a file called composer.json with this code inside: `{}`
4. Add `git add . ` and commit `git commit -m "heroku ready"` your changes 
5. Push your changes `git push -u origin master`

You should see these new files on Github.

## 4. Deploy to Heroku

There are two ways to deploy your code to Heroku. Either through the command line or through the web interface. We will walk you through both

### A. Through the Web interface
1. After logging into Heroku, create a new app 
2. Once created, go to the Deploy section and under Deployment Method, select Github
3. Connect your Github account and grant Heroku the permissions it needs. You should see your Github username and a input field beside it that asks for repo-name along with a search button
4. Click on Search and then Connect the repo you just created on Github from the list
5. Scroll all the way down to Manual Deploy and click on Deploy Branch. A build log will show up. Wait for it to finish.
6. Once it's done, click on the view button to see your website

### B. Through the terminal

For this method, we will need another software called Heroku CLI. You can find instructions on how to set it up [here](https://devcenter.heroku.com/articles/heroku-cli)

Once you have that installed:

1. Open a terminal window
2. Login to your Heroku account by running `heroku login` and entering your credentials
3. Navigate to the root folder of your project
4. Create a new heroku app: `heroku create YOURAPPNAME`
5. Deploy your code: 'git push heroku master'
6. Make sure that at least one server is running: `heroku ps:scale web=1`
7. View your website in the browser: `heroku open`

## And you are done :D
