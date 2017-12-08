# README: Pre-requirements, Installation and Deployment

**A - Pre-requirements**

* Ruby 2.3+
* Git
* PostgreSQL

**B - Installation (Cloud9)**

## 1 Install packages required to compile Thredded dependencies by running:

```
sudo apt-get install autoconf automake bison build-essential gawk git \
libffi-dev libgdbm-dev libgmp-dev libncurses5-dev libpq-dev libreadline6-dev \
libsqlite3-dev libtool libyaml-dev nodejs pkg-config ruby sqlite3
```

### 1.5 (optional) If you get an error: *Unable to fetch some archives, maybe run apt-get update or try with --fix-missing?*

Run: 
```
sudo apt-get update
```

## 2 Install the gem and create your app:
```
gem install thredded_create_app
```

You should see an output similar to:

> Fetching: thredded_create_app-0.1.22.gem (100%)
Successfully installed thredded_create_app-0.1.22
1 gem installed

## 3 Start PostgreSQL on Cloud9

Run:
```
sudo service postgresql start
```

Success output:

>  * Starting PostgreSQL 9.3 database server
   ...done.

## 4 Create your app

Run:
```
thredded_create_app app
```

Success:
> All done! 🌟

Escape with CTRL+C, cd into the app and run it on Cloud9:
```
cd app
rails s -b $IP -p $PORT
```

Point your browser to *http://workspacename-username.c9users.io/* (use your workspace name and user) to preview your application.

**C - Deployment (Github + Heroku)**

## 5 Create a git repository and add it:

```
git remote add origin https://github.com/username/repo.git
```

## 6 Initial push

```
git add .
git commit -m "initial push"
git push origin master
```

## 7 Create a new Heroku app first

## 8 Install Heroku CLI & log-in to your account

```
wget -qO- https://cli-assets.heroku.com/install-ubuntu.sh | sh
heroku login
```

## 9 Add the remote (replace repo with your actual repository name)

```
heroku git:remote -a repo
```

Success:
> set git remote heroku to https://git.heroku.com/repo.git

## 10 Set up database and seed data 

```
heroku run rake db:migrate db:seed
```
Now you can log-in with:

> email: admin@<app name>.com
> password: 123456

## 11 Set up email via the Mailgun Heroku add-on

## 11.1 Set the APP_HOST environment variable on Heroku so that the app knows its domain:

```
heroku config:set APP_HOST='e.g. myapp.herokuapp.com'
```
## 11.2 Enable Mailgun add-on (free plan)

```
heroku addons:create mailgun:starter
```

## 11.3 Copy the following snippet into config/environments/production.rb:

```
config.action_mailer.perform_deliveries = true
config.action_mailer.raise_delivery_errors = true
config.action_mailer.delivery_method = :smtp
config.action_mailer.smtp_settings = {
    domain: Settings.hostname,
    port: ENV['MAILGUN_SMTP_PORT'],
    address: ENV['MAILGUN_SMTP_SERVER'],
    user_name: ENV['MAILGUN_SMTP_LOGIN'],
    password: ENV['MAILGUN_SMTP_PASSWORD'],
    authentication: :plain,
}
```

Set the `domain` in the snippet above to your domain.

Commit and push to Heroku. You're all set!





