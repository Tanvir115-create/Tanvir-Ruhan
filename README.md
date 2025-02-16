create database project_hr;
use project_hr;
create table student(
ROLL int,
FNAME varchar(20),
LNAME varchar(20),
Marks int,
unique(ROLL,FNAME)
);
insert into student values(1,'Radha','Gupta',88);
insert into student values(2,'Shita','Gupta',89);
insert into student values(null,'Shita','Gupta',89);
insert into student values(null,'Shyam','Gupta',89);
select * from student;
drop table student;
create table student(
ROLL int,
FNAME varchar(20),
LNAME varchar(20),
Marks int,
primary key(ROLL,FNAME)
);
insert into student values(1,'Radha','Gupta',88);
insert into student values(2,'Radha','Gupta',88);-- allowed primary key different 
insert into student values(null,'Radha','Gupta',88); -- null not allowed 
drop table student;
create table student(
ROLL int,
MOBILE varchar(20),
FNAME varchar(20),
LNAME varchar(20),
Marks int,
primary key(ROLL,MOBILE) -- 2 primary key = composite key
);
insert into student values(1,'9988774455','Radha','Gupta',88);
insert into student values (2,'9988774455','Radha','Gupta',88);
insert into student values (2,'9988774456','Radha','Gupta',88); 
create table department(
Dept_id int primary key,
Dept_name varchar(20)
);

create table employee(
empid int primary key,
EMP_NAME varchar(20),
dept_id int,
foreign key(dept_id) references department(dept_id)
);
insert into department values(1,'IT');
insert into department values (2,'HR'); 
insert into department values (3,'Payroll'); 
insert into department values (4,' Admin'); 
insert into department values (5,'CSE'); 
select * from department;
insert into employee values(1,'Mark',1); 
insert into employee values(2,'John',1); 
insert into employee values(3,'Mike',1); 
insert into employee values(4,'Mary',2); 
insert into employee values(5,'Stacy',2); 
insert into employee values(6,'Radha',5);
insert into employee values(7,'Newaz',7);-- in dep_id 7 does not exist
select * from employee;
delete from department where dept_id =1; -- parent tables values cannot delate or update
delete from  department where dept_id =4; -- emp_id have not dept_id =4 we cannot use it
delete from  employee where dept_id =5; 
delete from  department where dept_id =5; 
insert into employee values(6,'Shyam',null); -- null is allowed in foreign key but not in primary key 
drop table employee; -- at first delete child table 
drop table department;-- we cannot delete parent table before child table 
create table department( 
Dept_id int primary key, 
Dept_name varchar(20) 
);-- parent table  
create table employee  
(empid int primary key, 
EMP_NAME varchar(20), 
dept_id int, 
foreign key(dept_id) references department(dept_id) on delete cascade on update cascade 
); -- child table 
insert into department values (1,'IT'); 
insert into department values (2,'HR'); 
insert into department values (3,'Payroll'); 
insert into department values (4,'Admin');

insert into employee values(1,'Mark',1); 
insert into employee values(2,'John',1); 
insert into employee values(3,'Mike',1); 
insert into employee values(4,'Mary',2); 
insert into employee values(5,'Stacy',2); 
select * from department;
select * from employee; -- here also delete the parent table data 
-- we will added cascade in child table 
delete from department where dept_id=1;
drop table employee;
drop table department;
update department set dept_id =5 where dept_name='IT';
alter table employee
add salary int check(salary between 500 and 5000);
update employee set salary =4000 where EMP_NAME='Mark'; 
alter table employee 
add gender varchar(20) check(gender in('Male','Female'));
update employee set gender ='Male' where EMP_NAME='Mark'; 
create table Orders(
ID int not null,
OrderNumber int not null,
OrderDate date default(current_date)
);
select * from Orders;

insert into Orders(ID,OrderNumber,OrderDate) values(1,001,'2023-05-10'); 
insert into Orders(ID,OrderNumber) values(1,001);
alter table employee 
add emp_status varchar(20) default "Not Joined";
select * from employee;
insert into employee(empid,EMP_NAME,dept_id,salary,gender) 
values(8,"Ramesh",3,700,"Female"); 
insert into employee(empid,EMP_NAME,dept_id,salary,gender,emp_status) 
values(10,"Rumel",4,800,"Male","Joined"); 
drop table orders;

create table Orders ( 
ID int  primary key auto_increment, 
OrderNumber int not null,  
OrderDate date DEFAULT(CURRENT_DATE) 
); 
insert into Orders(OrderNumber,OrderDate) values(001,'2023-05-10'); 
select * from Orders;
insert into Orders(OrderNumber) values(001); 
insert into Orders(OrderNumber,OrderDate) values(002,'2024-06-11'); 
insert into Orders(OrderNumber) values(003); 

select current_date();
-- Aggregate function ,update,delete,commit ,rollback
create database wscube;
use wscube;
create table students( 
id  int not null primary key , 
name varchar(64), 
email varchar(64), 
gender varchar(64), 
age int, 
city varchar(64), 
fees decimal(12,2)); 
insert into students values(1,"Bhagirath","bhgirath@wscube.com","M",23,"Jodhpur",5000.00); 
insert into students values(2,"Ravi","ravi@wscube.com","M",19,"Jaipur",6000.00); 
insert into students values(3,"Ramesh","ramesh@wscube.com","M",24,"Delhi",10000.00); 
insert into students values(4,"Pradeep","pradeep@wscube.com","M",31,"Udaipur",4000.00); 
insert into students values(5,"Kushagra","kushagra@wscube.com","M",23,"Jodhpur",8000.00); 
insert into students values(6,"Riya","riya@wscube.com","F",22,"Delhi",5000.00); 
select * from students;

-- Count() function--
select count(id) from students where fees>5000;
-- sum() function --
select sum(fees) from students;
-- avg()average function--
select avg(fees) from students;
select avg(fees) as 'avgFees' from students;
select min(fees) from students;
select max(fees) from students;
select max(age) from students;
select min(age) as 'child' from students;
select * from students;
-- update function--
update students set age = 20 where id = 2;
-- delete function--
delete from students where id = 4;
delete from students where id in (5,6);
insert into students values(7,"Aman","aman@wscubetech.com","M",23,'sylhet',5000); 
commit;
update students set fees = 15000 where id = 1;
rollback;
delete from students where id = 1;
commit;
rollback;
-- Arithmetic Operator--
create database employee;
use employee;
drop table EMP_INFO;
create table EMP_INFO(
ID int not null unique auto_increment,
NAME varchar(64),
JDATE date,
SAL decimal(10,2),
GENDER varchar(64)
);
select * from EMP_INFO;
insert into EMP_INFO(NAME,JDATE,SAL,GENDER) values('Surendra','2019-10-22',2500,"Male"); 
insert into EMP_INFO(NAME,JDATE,SAL,GENDER) values('Priyanka','2020-08-12',15500,"Female"); 
insert into EMP_INFO(NAME,JDATE,SAL,GENDER) values('Rahul','2018-07-28',28000,"Male"); 
insert into EMP_INFO(NAME,JDATE,SAL,GENDER) values('Zini','2018-02-21',75000,"Female"); 
insert into EMP_INFO(NAME,JDATE,SAL,GENDER) values('Jack','2021-05-09',45000,"Male"); 
insert into EMP_INFO(NAME,JDATE,SAL,GENDER) values('scott','2023-01-07',65000,"Female"); 
select * from EMP_INFO;
update EMP_INFO 
set SAL = 25000 where id = 1;

-- write a SQL Query to Display Employee name ,and annual salary of all employees 
select NAME,SAL,SAL*12 as 'Yearly Salary' from EMP_INFO;
-- write a SQL Query to Display Employee name ,and daily  salary of all employees
select NAME,SAL,SAL/30 as 'Daily Salary' from EMP_INFO;
--  Write a SQL Query to display Employee name ,salary and 10% of the salary as bonus . 
select NAME,SAL,SAL*0.10 as'10% Bonus 'from EMP_INFO;
--  Write a SQL Query to display Employee name,salary and 5% of salary as TA. 
select NAME,SAL,SAL*0.05 AS 'TA' from EMP_INFO;
--  Write a SQL Query to display Employee name , salary as basic salary then display 3%  
-- as TA ,6% as DA,12% as HRA,8% as COMM, and final salary 
select NAME,SAL as 'Basic Salary',0.03*SAL as 'TA',0.06*SAL as 'DA',0.12*SAL as 'HRA',0.08*SAL as 'COMM',
(SAL+0.03*SAL+0.06*SAL+0.12*SAL+0.08*SAL) as 'Final Salary' from EMP_INFO;
-- combination Query 
select name,sal as "BASIC SALARY",12*sal as "Yearly Salary",sal/30 as "Daily 
Salary",0.10*sal as "Bonus", 
0.05*sal as "TA",0.06*sal as "DA",0.12*sal as "HRA",0.08*sal as 
"COMM",(sal+0.03*sal+0.06*sal+0.12*sal+0.08*sal) as "Final Salary" from EMP_INFO;

-- Relationl Operator --
select * from emp_info;
-- write a SQL Query to display employee details having salaries less than 25,000 
select * from emp_info where sal<25000;
-- write a SQL Query to display employee having salaries less than or equal to 25,000
select * from emp_info where sal<=25000;
-- write a SQL Query to display employee detail having salaries equal to 75000
select * from emp_info where sal = 75000; 
-- write a SQL Query to display employee details those are not getting 28000.
select * from emp_info where sal!=28000;
-- write a SQL Query to display employee details whose name is Priyanka 
select * from emp_info where name = 'Priyanka'; 
-- write a SQL Query to display employee details who joined on 21st  feb 2021 
select * from emp_info where JDATE = '2021-02-21';
-- write a SQL Query to display employee details  who does not joined on 21st feb 2021 
select * from emp_info where JDATE!=2021-02-21;

-- Logical Operator --
-- Write a SQL queries to display employee detail those who are getting a salary greater 
-- than 25000 and gender is female 
select * from emp_info 
where(sal>25000 and gender ='Female');
-- Write a SQL queries to display employee details those who are getting salary between 
-- 30000 and 50000. 
select * from emp_info 
where(sal>30000 and sal<50000);
-- Write a SQL queries to display employee details those who have joinde after 
-- December 17th,2019 or are getting salary greater than 25000 
select * from emp_info 
where(JDATE>'2019-12-12'OR SAL>25000);
-- Write a SQL queries to display employee details those who are getting salary greater 
-- than 25000 and gender male or those who are getting salary  greater 30000 
select * from emp_info where(sal>25000 and gender = 'Male') or (sal>30000);
-- Write a SQL queries to display employee details for those who have not joined on oct 
-- 2nd 2022.
select * from emp_info where(JDATE!='2022-10-02');
select * from emp_info where(JDATE !='2018-07-28');
select * from emp_info where(JDATE ='2018-07-28');
-- set operators(union,union all,intersection,except---
create database Bank;
use Bank;
create table employees(
id int not null,
name varchar(64),
salary decimal(10.2),
department varchar(64),
dob date 
);
insert into employees values(101,'Jack',2000,'HR','1997-05-19'); 
insert into employees values(102,'Jack',NULL,'HR',NULL); 
insert into employees values(103,'Mack',6000,'Developer','1997-03-10'); 
insert into employees values(104,'Peter',4000,'Tester','1998-07-16'); 
insert into employees values(105,'Tom',3000,'HR','1998-11-03'); 
insert into employees values(106,'Leo',2500,'Developer','1997-10-10'); 
insert into employees values(107,'Roger',5300,'Accounts','1997-06-17'); 
insert into employees values(108,'Mike',2000,null,'1998-03-09'); 
insert into employees values(109,'Paul',4800,'Devoloper','1998-12-28'); 
insert into employees values(110,'Hannah',2000,'Accounts','1999-09-26'); 
select * from employees;
create table manager (
id int,
name varchar(64),
salary decimal(10,2),
department varchar(64),
dob date
);

insert into manager values(101,'Nancy',4000,'HR','1999-12-30'); 
insert into manager values(102,'Lucky',6500,'HR','1995-09-09'); 
insert into manager values(103,'Mack',6000,'Developer','1997-03-10'); 
insert into manager values(104,'Charlie',9500,'Tester','1998-06-24'); 
insert into manager values(105,'Tom',3000,'HR','1998-11-03'); 
select * from manager;
select * from employees;

select * from employees
union 
select * from manager;

select * from employees
union all
select * from manager;
-- Write a SQL queries to fetch all the details of  the employees who are not manager from the employee table 
select * from employees
except
select * from manager;
-- write a SQL query to return all the details of the  employees from the employee table who are manager 
select * from employees -- common only 
intersect
select * from manager;
select * from employees where id>104 -- common only 
intersect
select * from manager;

-- where Clause --
use wscube;
create table student(
id int primary key auto_increment,
name varchar(64),
email varchar(64),
age int,
city varchar(64)
);
insert into student values(1,"Bhagirath","bhagirath@wscubetech.com",23,"Jodhpur"); 
insert into student values(2,"John","John@wscubetech.com",18,"New York"); 
insert into student values(3,"Jenny","jenny@wscubetech.com",19,"Jaipur"); 
insert into student values(4,"Ramesh","ramesh@wscubetech.com",20,"Delhi"); 
insert into student values(5,"Deepil","deepil@wscubetech.com",25,"Bhopal"); 
select * from student;
select id,name,age from student;
select id,name as "Student name",age from student;
select id,name as "Student name",age as "Age"from student; -- we can renaeme columns name by using as 
select * from student where age>20;
select * from student where age<20;
select * from student where age=20;
select * from student where age!=20;
select * from student where age>=20;
select * from student where age>30;
select * from student where name = 'Bhagirath';
select * from student where name != 'Bhagirath';

-- where clause is used to filter records --
create table students(
id int primary key auto_increment not null unique,
name varchar(100),
email varchar(150) not null unique,
age tinyint check(age>=18),
city varchar(64),
gender varchar(3),
status boolean default 1
);
select * from students;
insert into students(name,email,age,city,gender) values("Bhagirath","bhagirath@wscubetech.com",23,"Jaipur","M"); 
insert into students(name,email,age,city,gender)  values("John","john@wscubetech.com",26,"Jaipur","M"); 
insert into students(name,email,age,city,gender)  values("Ankur","ankur@wscubetech.com",19,"Delhi","M"); 
insert into students(name,email,age,city,gender)  values("Jonny","jonny@wscubetech.com",20,"Agra","F"); 
insert into students(name,email,age,city,gender)  values("Jenny","jenny@wscubetech.com",21,"Jodhpur","F"); 
insert into students(name,email,age,city,gender)  values("Ashish","ashish@wscubetech.com",25,"Agra","M"); 
insert into students(name,email,age,city,gender)   values("Pradeep","pradeep@wscubetech.com",28,"Jodhpur","M"); 
insert into students(name,email,age,city,gender)  values("Riya","riya@wscubetech.com",30,"Agra","F"); 
insert into students(name,email,age,city,gender)  values("Kushargra","kushargra@wscubetech.com",35,"Jodhpur","M"); 
select * from students;
select * from students
where age>=18 and age<=25;
select * from students
where age  between 18 and 25;
select * from students
where age>=18 and age<=25 and city ='agra';
select * from students
where age>=18 and age<=25 and city ='agra' and gender ="M";
insert into students(name,email,age,city,gender)  values("Ravi","ravi@wscubetech.com",23,"Agra","M"); 
select * from students
where city ="Agra" or city ="Jodhpur";
select * from students
where city !="Agra";
select * from students
where not  city="Agra" or not  city="Jodhpur";


select * from students
where not  city="Agra" or not  city="Jodhpur";

-- in operator is used to the replace or --
select * from students 
where age =20 or age =21;
select * from students
where age = 20 or age =21 or age =23;
select * from students 
where age in(19,21,23);
select * from students where city in("Jodhpur","Jaipur");
-- like and wilcard operator //searching with like --
select * from students;
select * from students 
where name like "%a";-- ends with a 
select * from students 
where name like "a%"; -- starts with a 
select * from students 
where name like "%a%"; -- name with a in any wherw 
select * from students 
where name like "a____";-- start with a and have carry  5
select * from students 
where name like "a_____";-- start with a and have carry  6
select * from students 
where name like "a____%";-- start with a and have carry at least 5 charecter and at last something or nothing 
select * from students
where name like "%_a_%"; -- start with at least one charecter without a and end 
-- with at least one character and contain a in any where 
select * from students
where name like "r%a"; -- name start with r and ends with a 
select * from students 
where name like "%ku%"; -- contain ku in any where in name 
select * from students 
where name like "_r%";-- contain r in any where with out starting and ending 
-- between and not between operation/range operation --
select * from students 
where age between 20 and 25;-- give the records whose age is between 20 and 25 
select * from students 
where age  not between 20 and 25;
select * from students;
select * from students 
where name between "Bhagirath" and "Ashish";
-- order by/distrinct sorting ascending or discending--
select * from students 
order by name asc;
select * from students 
order by name desc;
select * from students 
order by age asc;
select * from students 
order by age desc;
-- distinct --
select distinct city from students; -- only city uniquely 
select distinct age from students;-- only ase uniquely 
select distinct age from students order by age asc;-- select age uniquly with ascending sorting 
select distinct age from students order by age desc;
select distinct city from students order by city asc;
select distinct city from students order by city desc;
insert into students values(11,'Shaili','sahili@wscube.com',24,'Jodhpur',null,1); 
insert into students values(12,'Jenny John','jennyjohn@wscube.com',20,null,null,1); 
select * from students;
select * from students 
where gender is null;
select * from students 
where gender is not  null;
select * from students 
where gender is null and city is null;
-- limit  --
select * from students;
select * from students limit 5;
select * from students order by name desc limit 5;
select * from students order by age desc limit 5;
select * from students where age>20 limit 5;
-- offset --
select * from students 
order by name desc;
select * from students limit 5 offset 0;
select * from students limit 5 offset 1;-- 2-6
select * from students limit 5 offset 2; -- 3-7
select * from students limit 5 offset 3;-- 4-8
select * from students limit 5 offset 5;
select * from students limit 5 offset 9;
use wscube;
create table city(
cid int not null auto_increment,
name varchar(64),
primary key(cid)
);
insert into city(name) values("Agra");
insert into city(name) values("Bhopal");
insert into city(name) values("Delhi");
insert into city(name) values("Jaipur");
insert into city(name) values("Rajkot");
select * from city;
create table students (
id int not null unique auto_increment,
name varchar(100) not null,
email varchar(100) not null,
city_id int not null,
primary key(id),
foreign key(city_id) references city(cid)
);
select * from students;
drop table students;
insert into students (name,email,city_id) values('A','a@wscubetech.com',1); 
insert into students (name,email,city_id) values('B','b@wscubetech.com',1); 
insert into students (name,email,city_id) values('C','c@wscubetech.com',2); 
insert into students (name,email,city_id) values('D','d@wscubetech.com',2);
insert into students (name,email,city_id) values('E','e@wscubetech.com',3); 
select * from students;
-- inner join 
select *from students
inner join city on students.city_id=city.cid; 
select * from students 
join city on students.city_id = city.cid; 
-- this is called inner join and join work same  
-- Left join --
select *from students
left join city on students.city_id=city.cid; -- all data from left table and matched data from right table 
-- right join --
select *from students
right join city on students.city_id=city.cid; -- all data from right  table and matched data from left table 

-- cross join --
select * from students 
cross join city;
select * from city 
cross join students;



 
