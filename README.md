# useful-when-it-needed

## Git
Return to Master and delete your commits that were not pushed yet
```
git reset master
```
## Linux

Find files in system
```
find . -name 'id-rsa*' -print
```
Create SSH Key
```
ssh-keygen -t rsa
id_rsa2
cat id_rsa2.pub
```
Send data retrive to a file
```
command > /directory/file_to_create
```
Generate random numbers from 20 to 30, retrive the 1st number on the list
```
shuf -i 20-30 -n 1
```
Number .txt lines
```
nl file_to_number.txt
```
## Docker
Dockerfile to implement diverse systems
```
version: '3'
services:
  jenkins:
    container_name: jenkins
    image: jenkins-ansible
    build:
      context: jenkins-ansible     
    ports:
      - "8080:8080"
    volumes:
      - $PWD/jenkins_home:/var/jenkins_home
    networks:
      - net
  remote_host:
    container_name: remote-host
    image: remote-host
    build:
      context: centos7
    volumes:
      - $PWD/aws-s3.sh:/tmp/script.sh
    networks:
      - net
  db_host:
    container_name: db
    image: mysql:5.7
    environment:
      - "MYSQL_ROOT_PASSWORD=1234"
    volumes:
      - $PWD/db_data:/var/lib/mysql
    networks:
      - net
  web:
    container_name: web
    image: ansible-web
    build:
      context: jenkins-ansible/web
    ports:
      - "80:80"
    networks:
      - net
  git:
    container_name: git-server
    image: 'gitlab/gitlab-ce:latest'
    hostname: 'gitlab.example.com'
    ports:
      - '8090:80'
    volumes:
      - '/srv/gitlab/config:/etc/gitlab'
      - '/srv/gitlab/logs:/var/log/gitlab'
      - '/srv/gitlab/data:/var/opt/gitlab'
    networks:
      - net
networks:
  net:
```
Dockerfile to implement tasks insideOS
```
FROM centos:7

RUN yum -y install openssh-server

RUN useradd remote_user && \
    echo "1234" | passwd remote_user  --stdin && \
    mkdir /home/remote_user/.ssh && \
    chmod 700 /home/remote_user/.ssh

COPY remote-key.pub /home/remote_user/.ssh/authorized_keys

RUN chown remote_user:remote_user   -R /home/remote_user && \
    chmod 400 /home/remote_user/.ssh/authorized_keys

RUN ssh-keygen -A

RUN yum -y install mysql

RUN yum -y install epel-release && \
    yum -y install python3-pip && \
    pip3 install --upgrade pip && \
    pip3 install awscli

CMD /usr/sbin/sshd -D
```
Start your dockerfile
```
docker-compoase up -d
```
Review podid
```
docker ps
```
Connect to docker instance
```
docker exec -it podid bash
```
Review pod log 
```
docker logs -f podid
```
## MySQL

Login to MySQL
```
mysql -u username -p password
```
Create DB
```
CREATE DATABASE DATABASE_NAME;
```
Create Table
```
USE DATABASE_NAME;
CREATE TABLE TABLE_NAME;
```
## AWS
Upload data to S3
```
aws s3 cp /tmp/file_to_upload s3:/bucket_name/upload_file_name
```
## Ansible
Excecute ansible actions
```
ansible -i host_file -m ping host_name
```
Excecute bash with Ansible
```
shell: excecute_linux_commands
```
Excecute Playbook with Ansible
```
ansible-playbook -i host_file yml_file.yml
```
## RPM
```
tar xf software-name.tar.gz
./configure
make
sudo make install
```
