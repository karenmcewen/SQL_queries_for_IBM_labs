# SQL_queries_for_IBM_labs
SQL queries used in my IBM online course labs
----------------------------------------------------
Lab#1 Instructors
create table INSTRUCTORS(ins_id  INT NOT NULL, 
lastname varchar(60) NOT NULL,
firstname varchar(60) NOT NULL,
city varchar(60),
country char(2),
primary key (ins_id )) ;

insert into INSTRUCTORS (ins_id, lastname, firstname, city, country) VALUES(1,'Ahuja', 'Rav', 'Toronto', 'CA');
insert into INSTRUCTORS (ins_id, lastname, firstname, city, country) 
VALUES(2,'Chong', 'Raul', 'Toronto', 'CA'),
(3,'Vasudevan', 'Hima', 'Chicago', 'US');

Select * from INSTRUCTORS;
Select firstname, lastname, country from INSTRUCTORS where city='Toronto';

Update INSTRUCTORS set city='Markham' where lastname = 'Ahuja';
Delete from INSTRUCTORS where firstname = 'Raul';

Select * from INSTRUCTORS;

------------------------------------
Lab 2.1 - Create Tables - HR Employers, Departments, etc.

------------------------------------------
--DDL statement for table 'HR' database--
--------------------------------------------

CREATE TABLE EMPLOYEES (
                            EMP_ID CHAR(9) NOT NULL, 
                            F_NAME VARCHAR(15) NOT NULL,
                            L_NAME VARCHAR(15) NOT NULL,
                            SSN CHAR(9),
                            B_DATE DATE,
                            SEX CHAR,
                            ADDRESS VARCHAR(30),
                            JOB_ID CHAR(9),
                            SALARY DECIMAL(10,2),
                            MANAGER_ID CHAR(9),
                            DEP_ID CHAR(9) NOT NULL,
                            PRIMARY KEY (EMP_ID));
                            
  CREATE TABLE JOB_HISTORY (
                            EMPL_ID CHAR(9) NOT NULL, 
                            START_DATE DATE,
                            JOBS_ID CHAR(9) NOT NULL,
                            DEPT_ID CHAR(9),
                            PRIMARY KEY (EMPL_ID,JOBS_ID));
 
 CREATE TABLE JOBS (
                            JOB_IDENT CHAR(9) NOT NULL, 
                            JOB_TITLE VARCHAR(15) ,
                            MIN_SALARY DECIMAL(10,2),
                            MAX_SALARY DECIMAL(10,2),
                            PRIMARY KEY (JOB_IDENT));

CREATE TABLE DEPARTMENTS (
                            DEPT_ID_DEP CHAR(9) NOT NULL, 
                            DEP_NAME VARCHAR(15) ,
                            MANAGER_ID CHAR(9),
                            LOC_ID CHAR(9),
                            PRIMARY KEY (DEPT_ID_DEP));

CREATE TABLE LOCATIONS (
                            LOCT_ID CHAR(9) NOT NULL,
                            DEP_ID_LOC CHAR(9) NOT NULL,
                            PRIMARY KEY (LOCT_ID,DEP_ID_LOC));
                            
--------------------------------------------------------------------
Lab week 2.1 - SQL queries 
 
select f_name, l_name from employees where address like '%Elgin,IL%';
select * from employees;
select f_name, l_name from employees where b_date like '197%';
select f_name, l_name from employees where salary between 60000 and 70000;
select f_name, l_name, dep_id from employees order by dep_id desc , l_name desc;
select dep_id, count(dep_id) as num_employees , avg(salary)  as  avg_salary from employees group by dep_id having count(dep_id) <4 order by avg(salary);

---------------------------------------------------------------------
Lab - PETSALE - Create tables

-- Drop the PETSALE table in case it exists
drop table PETSALE;
-- Create the PETSALE table 
create table PETSALE (
	ID INTEGER PRIMARY KEY NOT NULL,
	ANIMAL VARCHAR(20),
	QUANTITY INTEGER,
	SALEPRICE DECIMAL(6,2),
	SALEDATE DATE
	);
-- Insert saple data into PETSALE table
insert into PETSALE values 
	(1,'Cat',9,450.09,'2018-05-29'),
	(2,'Dog',3,666.66,'2018-06-01'),
	(3,'Dog',1,100.00,'2018-06-04'),
	(4,'Parrot',2,50.00,'2018-06-04'),
	(5,'Dog',1,75.75,'2018-06-10'),
	(6,'Hamster',6,60.60,'2018-06-11'),
	(7,'Cat',1,44.44,'2018-06-11'),
	(8,'Goldfish',24,48.48,'2018-06-14'),
	(9,'Dog',2,222.22,'2018-06-15')
	
;

-----------------------------------------------
Lab - PETSALE - functions

select SUM(SALEPRICE) from PETSALE;
select SUM(SALEPRICE) AS SUM_OF_SALEPRICE from PETSALE;
select MAX(QUANTITY) from PETSALE;
select AVG(SALEPRICE) from PETSALE;
select AVG( SALEPRICE / QUANTITY ) from PETSALE where ANIMAL = 'Dog';
select ROUND(SALEPRICE) from PETSALE;
select LENGTH(ANIMAL) from PETSALE;
select UCASE(ANIMAL) from PETSALE;
select DISTINCT(UCASE(ANIMAL)) from PETSALE;
select * from PETSALE where LCASE(ANIMAL) = 'cat';
select DAY(SALEDATE) from PETSALE where ANIMAL = 'Cat';
select COUNT(*) from PETSALE where MONTH(SALEDATE)='05';
select (SALEDATE + 3 DAYS) from PETSALE;
select (CURRENT DATE - SALEDATE) from PETSALE;

---------------------------------------------------
Lab - PETSALE - SQL queries

select * from petsale;
select * from PETSALE where ANIMAL = 'Dog' ;
select avg(saleprice/quantity) from petsale where lower(animal) = 'dog';
select animal, ROUND (SALEPRICE) as cost from PETSALE;

------------------------------------------------------

Lab - subqueries - uses HR tables from lab 2.1

select * from employees, departments;
select * from employees where dep_id in ( select dept_id_dep from departments); 
select * from employees, departments where employees.dep_id = departments.dept_id_dep;
select * from employees E, departments D where E.DEP_ID = D.DEPT_ID_DEP;
select E.EMP_ID, D.DEPT_ID_DEP from employees E, departments D where E.DEP_ID = D.DEPT_ID_DEP;

------------------------------------------------------------


