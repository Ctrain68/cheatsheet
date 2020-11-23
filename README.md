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

#### Change Python version
```bash
sudo update-alternatives --install /usr/bin/python python /usr/bin/<python version>
sudo update-alternatives --install /usr/bin/python python /usr/bin/<python version>
```
This updates the pointers for python3


#### Change default Python3

```bash
sudo update-alternatives --config python
```

Select Appropriate Python that you want ad default

#### Install PIP for python packages

```bash
apt-get install python3-pip
```

#### Instal python module for Virtual Environment

```bash
apt-get install python3-venv
```

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
WorkingDirectory=/home/ubuntu/{code-folder}
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
* create a role in AWS to grant access to S3 buckets / other services - S3 Read only is a preset
* use aws cli to be able to download and copy file from s3 bucket
```bash
$ curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64-2.0.30.zip" -o "awscliv2.zip"
unzip awscliv2.zip
```
```bash
sudo ./aws/install
```
Note that unzip may have to be installed

* Add env file to EC2 instance 

```bash
aws s3 cp s3://{s3-bucket-name}/{folder}/{file} /home/ubuntu/{code-folder}/{file-name}

* write a bash script to:
    * copy the env file from the S3 bucket to your code
    * start up Gunicorn 
```bash
#!/bin/bash

/usr/local/bin aws s3 cp s3://col-flask-app-image-lesson/environment/.env /home/ubuntu/ccc-03-16/.env
cd ccc-03-16
/home/ubuntu/.local/bin/gunicorn -b 0.0.0.0:5000 -w 3 "main:create_app()"
```



* Alter SystemD file to run the bash script


```bash
[Unit]
Description=Gunicorn managing flask application
After=network.target

[Service]
#EnvironmentFile=/home/ubuntu/.env
User=ubuntu
WorkingDirectory=/home/ubuntu/ccc-03-16
ExecStart=/homr/ubuntu/booth.sh
Restart=always

[Install]
WantedBy=multi-user.target
```

## Docker

### Download docker image (eg ubuntu)

```bash
docker pull <image>
```

### Run docker container with name

```bash
docker run -d -t --name <name> <docker_image>
```
OR
```bash
docker run -d -t -p 80:80 --name <name> <docker_image>
```
 Where the -p command is for port. The last number is for the docker container. The first 80 for the host.
### connect  to Docker os

```bash
docker exec -it <name> <terminal_shell>
```

### Running Containers

```bash
docker ps
```