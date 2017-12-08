# README

**Pre-requirements**

* Ruby 2.3+
* Git
* PostgreSQL

#**Installation (Cloud9)**

##1 Install packages required to compile Thredded dependencies by running:

> sudo apt-get install autoconf automake bison build-essential gawk git \
  libffi-dev libgdbm-dev libgmp-dev libncurses5-dev libpq-dev libreadline6-dev \
  libsqlite3-dev libtool libyaml-dev nodejs pkg-config ruby sqlite3

###1.5 (optional) If you get an error: *Unable to fetch some archives, maybe run apt-get update or try with --fix-missing?*

Run: 
> sudo apt-get update

##2 Install the gem and create your app:

> gem install thredded_create_app

You should see an output similar to:

> Fetching: thredded_create_app-0.1.22.gem (100%)
Successfully installed thredded_create_app-0.1.22
1 gem installed

##3 Start PostgreSQL on Cloud9

Run:
> sudo service postgresql start

Success output:

>  * Starting PostgreSQL 9.3 database server
   ...done.

##4 Create your app

Run:
> thredded_create_app app

Success:
> All done! 🌟

Escape with CTRL+C, cd into the app and run it on Cloud9:

> cd app
> rails s -b $IP -p $PORT

Point your browser to *http://workspacename-username.c9users.io/* (use your workspace name and user) to preview your application.

