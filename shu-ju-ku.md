 CREATE USER 'hello'@'%' IDENTIFIED WITH mysql_native_password BY '528136'
 
 flush privileges;
 
 grant all privileges on *.* to 'hello'@'%';
 
 flush privileges;