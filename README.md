# Sqoop-Multithreading-Import
This repository gives the clear explanation/steps on how to change the --m 1 in Sqoop import.

# Go to the Mysql and run following query and insert data into the table customer_mapper

     use test;

     CREATE TABLE customer_mapper(custid INT,firstname VARCHAR(20),lastname VARCHAR(20),city varchar(50),age int,createdt date,transactamt int );

     insert into customer_mapper values(1,'Arun','Kumar','chennai',33,'2015-09-20',100000);
     insert into customer_mapper values(2,'srini','vasan','chennai',33,'2015-09-21',10000);
     insert into customer_mapper values(3,'vasu','devan','banglore',39,'2015-09-22',90000);
     insert into customer_mapper values(4,'mohamed','imran','hyderabad',33,'2015-09-23',1000);
     insert into customer_mapper values(5,'arun','basker','chennai',23,'2015-09-24',200000);
     insert into customer_mapper values(6,'arun','basker','chennai',23,'2015-09-24',200000);
     insert into customer_mapper values(7,'arun','basker','chennai',23,'2015-09-24',200000);
     insert into customer_mapper values(8,'arun','basker','chennai',23,'2015-09-24',200000);
     insert into customer_mapper values(9,'arun','basker','chennai',23,'2015-09-24',200000);
     insert into customer_mapper values(10,'arun','basker','chennai',23,'2015-09-24',200000);


# Go to the Edge Node and run sqoop import command

     sqoop import \
     --connect jdbc:mysql://localhost/test \
     --username root \
     --password <> \
     --table customer_mapper \
     -m 1  \
     --delete-target-dir \
     --target-dir /user/cloudera/mapper_data

# Go to the HDFS and run the following command

     hadoop fs -ls /user/cloudera/mapper_data ==>( One part File)

# Go to the edge node and run sqoop import command
     
     sqoop import \
     --connect jdbc:mysql://localhost/test \
     --username root \
     --password <> \
     --table customer_mapper \
     -m 2 --split-by custid  \
     --delete-target-dir \
     --target-dir /user/cloudera/mapper_data      

# Go to the HDFS 

     hadoop fs -ls /user/cloudera/mapper_data ==> It gives TWO Part  Files

# Go to the edge node and run the following command (sqoop import)
     
     sqoop import \
     --connect jdbc:mysql://localhost/test \
     --username root \
     --password <> \
     --table customer_mapper \
     --split-by custid  \
     --delete-target-dir \
     --target-dir /user/cloudera/mapper_data      

# Go to the HDFS and run the following command
hadoop fs -ls /user/cloudera/mapper_data ===> It gives FOUR or FIVE Part Files
