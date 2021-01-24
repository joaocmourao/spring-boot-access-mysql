# spring-boot-access-mysql
Access mysql using spring-boot

<h1>Prerequisites:</h1>
->mysql database

<p>Using docker to get mysql database:</p>
<p>1-get mysql docker container:
docker run -p 3306:3306 --name=mysql57 -d mysql/mysql-server:5.7</p>
<p>2-get generated password</p>
docker logs mysql57 2>&1 | grep GENERATED
<p>3-connect mysql client using the password</p>
docker exec -it mysql57 mysql -uroot -p
<p>4-change root password</p>
ALTER USER 'root'@'localhost' IDENTIFIED BY 'NEW_USER_PASSWORD';
FLUSH PRIVILEGES;
<p>5-set the host</p>
update mysql.user set host = '%' where user='root';
<p>6-restart container</p>
docker restart mysql57

You will now be able to connect to mysql running on docker using mysql workbench client.

Before running the project you must create a database and user for the application to use it:
<p>create database db_example; -- Creates the new database
<p>create user 'springuser'@'%' identified by 'ThePassword'; -- Creates the user
<p>grant all on db_example.* to 'springuser'@'%'; -- Gives all privileges to the new user on the newly created database

When going to production change user privileges to 
<p>revoke all on db_example.* from 'springuser'@'%';
<p>grant select, insert, delete, update on db_example.* to 'springuser'@'%';
