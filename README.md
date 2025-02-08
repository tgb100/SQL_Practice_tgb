# SQL_Practice_tgb
tgb's SQL Practice
-- Database Operations for VIT
-- Show existing databases
SHOW DATABASES;

-- Create and use VIT database
CREATE DATABASE IF NOT EXISTS VIT;
USE VIT;

-- Create CSE table with improved structure
CREATE TABLE IF NOT EXISTS CSE (
    s_id INT PRIMARY KEY,
    s_name VARCHAR(30) NOT NULL,
    s_mark INT CHECK (s_mark BETWEEN 0 AND 100),
    s_country VARCHAR(50) DEFAULT 'India'
);

-- Verify table creation
SHOW TABLES;

-- Insert initial data
INSERT INTO CSE (s_id, s_name, s_mark) 
VALUES (70, 'jm', 78);

-- Table structure inspection
DESC CSE;

-- Column modifications
ALTER TABLE CSE 
ADD COLUMN address VARCHAR(200);

ALTER TABLE CSE 
DROP COLUMN address;

ALTER TABLE CSE 
RENAME COLUMN s_country TO s_state;

-- Safe update demonstration
SET SQL_SAFE_UPDATES = 0;
UPDATE CSE 
SET s_state = 'Belgium' 
WHERE s_id = 70;
SET SQL_SAFE_UPDATES = 1;

-- Transaction Practice Database
CREATE DATABASE IF NOT EXISTS practice1;
USE practice1;

CREATE TABLE IF NOT EXISTS Mech (
    s_id INT PRIMARY KEY,
    s_name VARCHAR(25)
);

-- Transaction with savepoints
START TRANSACTION;
INSERT INTO Mech VALUES (101, 'jayanth');
SAVEPOINT A;
UPDATE Mech SET s_id = 102 WHERE s_id = 101;
SAVEPOINT B;
INSERT INTO Mech VALUES (103, 'Karthick');
SAVEPOINT C;
ROLLBACK TO B;
COMMIT;

-- Organization Database Setup
CREATE DATABASE IF NOT EXISTS ORG;
USE ORG;

CREATE TABLE IF NOT EXISTS Worker (
    WORKER_ID INT PRIMARY KEY AUTO_INCREMENT,
    FIRST_NAME VARCHAR(25),
    LAST_NAME VARCHAR(25),
    SALARY INT,
    JOINING_DATE DATETIME,
    DEPARTMENT VARCHAR(25)
);

-- Insert data with corrected date format
INSERT INTO Worker (FIRST_NAME, LAST_NAME, SALARY, JOINING_DATE, DEPARTMENT) VALUES
('Monika', 'Arora', 100000, '2014-02-20 09:00:00', 'HR'),
('Niharika', 'Verma', 80000, '2014-06-11 09:00:00', 'Admin'),
('Vishal', 'Singhal', 300000, '2014-02-20 09:00:00', 'HR'),
('Amitabh', 'Singh', 500000, '2014-02-20 09:00:00', 'Admin'),
('Vivek', 'Bhati', 500000, '2014-06-11 09:00:00', 'Admin'),
('Vipul', 'Diwan', 200000, '2014-06-11 09:00:00', 'Account'),
('Satish', 'Kumar', 75000, '2014-01-20 09:00:00', 'Account'),
('Geetika', 'Chauhan', 90000, '2014-04-11 09:00:00', 'Admin');

-- Enhanced Queries
-- 1. Employees with salary > 200,000 in HR
SELECT * FROM Worker 
WHERE DEPARTMENT = 'HR' AND SALARY > 200000;

-- 2. Salary range query
SELECT * FROM Worker 
WHERE SALARY BETWEEN 200000 AND 500000;

-- 3. Department statistics
SELECT 
    DEPARTMENT,
    COUNT(*) AS employee_count,
    AVG(SALARY) AS avg_salary,
    MAX(SALARY) AS max_salary,
    MIN(SALARY) AS min_salary
FROM Worker
GROUP BY DEPARTMENT
ORDER BY employee_count DESC;

-- 4. Top 2 departments by employee count
SELECT DEPARTMENT, COUNT(*) AS employee_count
FROM Worker
GROUP BY DEPARTMENT
ORDER BY employee_count DESC
LIMIT 2;

-- 5. Department-wise maximum salaries using window functions
SELECT DISTINCT DEPARTMENT,
MAX(SALARY) OVER (PARTITION BY DEPARTMENT) AS max_salary
FROM Worker;

-- 6. Top 3 salaries in Admin department
SELECT * FROM Worker
WHERE DEPARTMENT = 'Admin'
ORDER BY SALARY DESC
LIMIT 3;

CREATE TABLE person1 (
    id INT PRIMARY KEY, 
    lastname VARCHAR(255) NOT NULL UNIQUE, 
    firstname VARCHAR(255) NOT NULL UNIQUE, 
    age INT
);

DESC person1;

INSERT INTO person1 (id, lastname, firstname, age) 
VALUES (1, 'Doe', 'John', 30);


SELECT * FROM person1;

create table category(
c_id int primary key,
c_name varchar(25) not null unique,
c_decrp varchar(250) not null
);

insert into category values (102, 'furnitures', 'it stores all set of wooden items');
select * from category;
desc category;

use org123;
CREATE TABLE Products (
    P_ID int primary key,
    p_Name varchar(250) NOT NULL,
    c_id int ,
    CONSTRAINT c_id FOREIGN KEY (c_id)
    REFERENCES category(c_id)
);
show tables from org123;
desc products;

drop table products;

insert into products values (904, 'Wooden table', null);
select * from products;


select * from category;

delete from category where c_id=101;

drop table category;

USE org123;


CREATE TABLE Student (
    sno INT PRIMARY KEY,
    sname VARCHAR(20),
    age INT

);


INSERT INTO Student(sno, sname,age) 
 VALUES(5,'skit',17),
       (7,'samya',18),
       (6,'samm',16);

SELECT *
FROM Student;

CREATE TABLE Course (
    cno INT PRIMARY KEY,
    cname VARCHAR(20)
);

SELECT *
FROM Course;

INSERT INTO Course(cno, cname) 
 VALUES(101,'c'),
       (102,'c++'),
       (103,'DBMS');

INSERT INTO Course(cno, cname) 
 VALUES(104,'c#'),
       (105,'java'),
       (106,'OS');

CREATE TABLE Enroll (
    sno INT,
    cno INT,
    jdate DATE,
    PRIMARY KEY(sno, cno),
    FOREIGN KEY(sno) REFERENCES Student(sno) ON DELETE CASCADE,
    FOREIGN KEY(cno) REFERENCES Course(cno) ON DELETE CASCADE
);

INSERT INTO Enroll(sno, cno, jdate) 
VALUES (1, 101, '2021-06-05'),
       (1, 102, '2021-06-05'),
       (2, 103, '2021-06-06');

SELECT * FROM Enroll;

DELETE FROM Student WHERE sname = 'Ramya';

SELECT * FROM Student;

SELECT * FROM Enroll;

INSERT INTO Enroll(sno, cno, jdate) 
VALUES(2, 105, "2021/05/05");
select * from enroll;
desc Enroll;

create database saturday;
use saturday;

create table category(
c_id int primary key,
c_name varchar(25) not null unique,
c_decrp varchar(250) not null
);

insert into category values (101, 'electronics', 'it stores all set of electronics items');
select * from category;
desc category;

CREATE TABLE Products (
    P_ID int primary key,
    p_Name varchar(250) NOT NULL,
    c_id int ,
    CONSTRAINT c_id FOREIGN KEY (c_id)
    REFERENCES category(c_id) on delete cascade
);

insert into products values (904, 'INTEL I5 Processor', 101);
select * from products;
delete from category where c_id=101;
select * from category;

CREATE TABLE Colleges (
    college_id INT PRIMARY KEY,
    college_name VARCHAR(50) NOT NULL
);

CREATE TABLE Subjects (
    subject_id INT PRIMARY KEY,
    subject_name VARCHAR(50) NOT NULL,
    college_id INT,
    FOREIGN KEY (college_id) REFERENCES Colleges(college_id) ON DELETE CASCADE
);

CREATE TABLE Students (
    student_id INT PRIMARY KEY,
    student_name VARCHAR(50) NOT NULL,
    college_id INT,
    subject_id INT,
    FOREIGN KEY (college_id) REFERENCES Colleges(college_id) ON DELETE CASCADE,
    FOREIGN KEY (subject_id) REFERENCES Subjects(subject_id) ON DELETE CASCADE
);

INSERT INTO Colleges (college_id, college_name) VALUES
    (1, 'VIT Bhopal'),
    (2, 'IIT Indore'),
    (3, 'NIT Warangal');

INSERT INTO Subjects (subject_id, subject_name, college_id) VALUES
    (1, 'Computer Science', 1),
    (2, 'Mathematics', 1),
    (3, 'Physics', 2),
    (4, 'Electrical Engineering', 3);

INSERT INTO Students (student_id, student_name, college_id, subject_id) VALUES
    (1, 'Rahul Sharma', 1, 1),
    (2, 'Priya Jain', 1, 2),
    (3, 'Amit Verma', 2, 3),
    (4, 'Sneha Rao', 3, 4);

SELECT * FROM Colleges;
SELECT * FROM Subjects;
SELECT * FROM Students;

