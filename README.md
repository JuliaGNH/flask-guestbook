This is used in the demonstration of development of Ansible Playbooks.

  Below are the steps required to get this working on a base linux system.

  - Install all required dependencies
  - Start Web Server

## 1. Install system dependencies

  Python and its dependencies

    apt-get install -y python python-setuptools python-dev build-essential python-pip python-mysqldb


## 2. Install application dependencies

Install python dependencies

    pip install flask
    pip install flask-sqlalchemy

## 3. Download the application
git clone https://github.com/ameade/flask-guestbook

## 4. Start Web Server
Ensure the application is not already running
  kill $(ps -ef |grep -v grep | grep -w flask |awk '{print $2}')
Start web server in a background process
    FLASK_APP=app.py nohup flask run &

## 5. Test
    curl http://<IP>:8080/signatures

# Add a mysql database

## 1. Install and Configure Database

 Install MySQL database

    apt-get install -y mysql-server mysql-client

## 2. Start Database Service
  - Start the database service

        service mysql start

  - Create database and database users

        # mysql -u <username> -p

        mysql> CREATE DATABASE guestbook;
        mysql> GRANT ALL ON *.* to db_user@'%' IDENTIFIED BY 'Passw0rd';

  - Configure database credentials and parameters for the app
        The app looks for a configuration file at '/opt/guestbook/vars.ini'
