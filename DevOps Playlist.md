DEVOPS


Git / Github
Docker / Docker Compose
Kubernetes
Terraform (Infrastructure as Code)
CI/CD Jenkins
Jenkins plugins
Ansible
Puppet
Prometheous / Grafana / Nagios

Programming
Python, Bash Shell scripting / PHP / Javascript / BAT / 


Git
Git clone, add, remote add, commit, push, pull, rebase, merge, log (Flags -d, -it)

Docker
Dockerfile 
Docker up, start, ps, image, docker stop, docker run, 

Docker-compose up, run (Flags -d, -it)

Installing Docker in Ubuntu VM
# sudo apt-get update
# Prerequisite
```
sudo apt-get install linux-image-extra-$(uname -r) linux-image-extra-virutal
```
## Install docker on Ubuntu
```
sudo apt-get  install docker-engine
```
## Start docker
```
sudo service docker start
```
## Pull image
```
sudo docker pull <image-name>
```
## Run container from image
```
sudo docker run -it <image-name>
```

## Docker Compose
### Install pip from python
```
sudo apt-get install python3-pip
```
Use pip to install docker-compose
```
sudo pip install docker-compose
```

## Creating docker-compose.yml configuration file
