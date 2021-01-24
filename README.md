# spring-boot-access-mysql
Access mysql using spring-boot

Prerequisites:
->mysql database

Using docker to get mysql database:
1-get mysql docker container:
docker run -p 3306:3306 --name=mysql57 -d mysql/mysql-server:5.7
2-get generated password
docker logs mysql57 2>&1 | grep GENERATED
3-connect mysql client using the password
docker exec -it mysql57 mysql -uroot -p
4-change root password
ALTER USER 'root'@'localhost' IDENTIFIED BY 'NEW_USER_PASSWORD';
FLUSH PRIVILEGES;
5-set the host
update mysql.user set host = '%' where user='root';
6-restart container
docker restart mysql57

You will now be able to connect to mysql running on docker using mysql workbench client.


