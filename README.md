## Bash

### Update repositries for Ubuntu

```bash
sudo apt update
```
### Update your software

```bash
sudo apt upgrade
```
### Install Package

```bash
sudo apt install <package>
```
### Install Package including required dependancies

```bash
sudo apt-get install <package>
```







## Python

### Python General commands


#### Update requirements file for python venv

```bash
pip freeze > requirements.txt
```

#### Install packages for python venv

```bash
 pip install -r requirements.txt
 ```










## Postgres

## Setup SystemD
```bash
sudo touch /etc/systemd/system/flaskapi.service
sudo vim /etc/systemd/system/flaskapi.service
```


### Example of a SystemD file for Gunicorn

```bash
[Unit]
Description=Gunicorn managing flask application
After=network.target

[Service]
EnvironmentFile=/home/ubuntu/.env
User=ubuntu
WorkingDirectory=/home/ubuntu/ccc-03-16
ExecStart=/home/ubuntu/.local/bin/gunicorn -b 0.0.0.0:5000 -w 3 "main:create_app()"
Restart=always

[Install]
WantedBy=multi-user.target



```

## Systemctl

### Status of an app

```bash
sudo systemctl status flaskapi
```

### Start an app

```bash
sudo systemctl start flaskapi
```

### Start a service when the instance(Ec@) is started

```bash
sudo systemctl enable flaskapi
```

### See all systemD units loaded

```bash
systemctl
```

### Reload Daemon for systemD

```bash
sudo systemctl daemon-reload
```


### Process running in linux sorted by usage
```bash
top -o PID
```
### Process sorted by threads running in linux 
```bash
top -p <PID> -H
```

### script for env variables s3

* upload file to S3 bucket - env file with variables
* create a role in AWS to grant access to S3 buckets / other services
* use aws cli to be able to download and copy file from s3 bucket
* write a bash script to:
    * copy the env file from the S3 bucket to your code
    * start up Gunicorn 
* Alter SystemD file to run the bash script
