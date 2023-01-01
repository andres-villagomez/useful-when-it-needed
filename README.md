# useful-when-it-needed
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
## Docker

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
