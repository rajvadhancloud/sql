# sql

-- creating database

CREATE database school;
create database if not exists school;

-- deleting database

drop database school;
drop database if exists school;

-- selecting a database to work upon

use school;

-- ceating a table with its columns

create table students(
	id int primary key unique, -- primary key is by default unique and null
    name varchar(50),
    age int not null default 20 -- sets default value
    -- primary key (id,name)
    constraint age_check check (age>=18 and age<=40)
);

create table student(
	rollno int primary key,
    name varchar(50),
    marks int not null,
    grade varchar(1),
    city varchar(20)
);

-- foriegn key example

create table dept(
	id int primary key,
    name varchar(50)
);

create table teacher(
	id int primary key,
    name varchar(50),
    dept_id int,
    foreign key (dept_id) references dept(id)
    on delete cascade -- deletes child also if deletion happens in parent
    on update cascade -- updates chid also if updation happens in parent
);

-- alter

alter table student 
add column age int not null default 20;  -- to add new column-- 

alter table student
drop column age; -- to delete column

alter table student_record
rename to student; -- to rename table name

alter table student
change column rollno roll_no int primary key; -- to replace column from another column

alter table student
modify column age int default 21; -- to modify pre added columns

-- creating records in table

insert into students values(1,"raj",21);
insert into students value(2,"shubham",23);
insert into students value(3,"vaibhav",22);
insert into students value(4,"suraj",25);
insert into students value(5,"vipul",23);
insert into students value(6,"sonu",24);

insert into students (id,name,age) values(7,"raju",18); 

insert into students values(1,"raj",21),(2,"shubham",23),(3,"vaibhav",22),(4,"suraj",25),(5,"vipul",23),(6,"sonu",24);

insert into student
values
(101,"anil",78,"C", "Pune"),
(102,"bhumika",93,"A","Mumbai"),
(103,"chetan",85,"B","Mumbai"),
(104,"dhruv",96,"A","Delhi"),
(105,"emanuel",12,"F","Delhi"),
(106,"farah",82,"B","Delhi");

insert into student (rollno,name,marks,grade,city) values
(107,"raj",99,"A","Goa"); 

insert into dept values 
(101,"maths"),
(102,"english");

insert into teacher values
(1,"mohit",102),
(2,"vineet",101);

-- truncate

truncate table student; -- deletes all records in table

-- deleting table

drop table students;
drop table teacher;
drop table dept;

-- show records

select * from students;
select * from student;
select name, marks from student;
select distinct city from student; -- to select unique items
select * from student where marks>80;
select name from student where city="mumbai";
select * from student where marks>80 and city="delhi";
select * from student where marks+10>100;
select * from student where marks between 80 and 90;
select * from student where city in("delhi","mumbai");
select * from student where city not in ("pune","mumbai");
select * from student limit 4;
select * from student where marks > 80 limit 2;
select * from student order by marks desc limit 3;
select * from student order by name asc;
select count(marks) from student;
select max(marks) from student;
select avg(marks) from student;
select city,count(name) from student group by city;
select city, avg(marks) from student group by city order by avg(marks) desc;
select grade, count(rollno) from student group by grade order by grade asc;
select city, grade, count(name) from student group by city, grade;
select grade, count(name) from student where grade="A";
select city, count(name) from student group by city having max(marks)>90;
select city, count(name) from student where marks>90 group by city;

select * from dept;
select * from teacher;

-- correct order of writing sql query

select city, count(name)
from student
where grade = "A" or grade = "B"
group by city
having max(marks)>=85
order by city desc;

-- update queries

set sql_safe_updates = 0; -- to turn off safe mode
set sql_safe_updates = 1; -- to turn on safe mode

update student set grade = "O" where grade = "A";
update student set marks = 75 where rollno = 105;
update student set grade = "C" where marks between 70 and 80;
update student set marks = marks + 1;

update dept set id = 104 where id = 101;

-- delete queries

delete from student; -- deletes whole data of table
delete from student where marks < 80;

-- show all databases

show databases;
 
 -- show all tables of use database
 
 show tables;

-- foriegn key

create table temp(
	stud_id int,
    foreign key (stud_id) references students(id)
);

drop table temp;

-- practice questions

-- Q1

create database xyz;
use xyz;
create table employee(
	id int primary key,
    name varchar(50),
    salary int
);
insert into employee values(1,"adam",25000),(2,"bob",30000),(3,"casey",40000);
select * from employee;

-- Q2

create database shop;
use shop;
create table customers(
	customer_id int primary key,
    customer varchar(50),
    mode varchar(30),
    city varchar(30)
);
insert into customers values
(101,"Oliva Barrett","Netbanking","Portland"),
(102,"Ethan Sinclair","Credit Card","Miami"),
(103,"Maya Hernandez","Credit Card","Seattle"),
(104,"Liam Donovan","Netbanking","Denver"),
(105,"Sophia Nguyen","Credit Card","New Orleans"),
(106,"Caleb Foster","Debit Card","Minneapolis"),
(107,"Ava Patel","Debit Card","Phoenix"),
(108,"Lucas Carter","Netbanking","Boston"),
(109,"Isabella Martinez","Netbanking","Nashville"),
(110,"Jackson Brooks","Credit Card","Boston");

select * from customers;
select mode, count(customer_id) from customers group by mode;

drop table customers;


















