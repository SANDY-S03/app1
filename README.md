
assi2
CREATE DATABASE LIBRARY;
USE LIBRARY;
DROP TABLE bookdata;
CREATE TABLE bookdata(
bookid INT PRIMARY KEY,
name VARCHAR(50),
author VARCHAR(50),
type VARCHAR(50),
UNIQUE(bookid, name,author),
UNIQUE (type,name,bookid),
UNIQUE(author, type)
);
INSERT INTO bookdata (bookid, name, author, type) VALUES (1, "alchemist","paulo_cohelo","adventure"),(2, "wings_of_fire","apj_abdul_kalam", "autobiography");
SELECT * FROM bookdata;


CREATE TABLE book_3nf_1(
bookid INT ,
name VARCHAR(50),
author VARCHAR(50),
PRIMARY KEY(bookid, name)
);
INSERT INTO book_3nf_1 (bookid, name, author) VALUES (1, "alchemist","paulo_cohelo"),(2, "wings_of_fire","apj_abdul_kalam");

CREATE TABLE book_3nf_2(
author VARCHAR(50) PRIMARY KEY,
type VARCHAR(50)
);
INSERT INTO book_3nf_2 (author, type) VALUES ("paulo_cohelo","adventure"),("apj_abdul_kalam", "autobiography");

CREATE TABLE book_bcnf_1(
bookid INT ,
name VARCHAR(50),
type VARCHAR(50),
PRIMARY KEY(type,name)
);


INSERT INTO book_bcnf_1 (bookid, name, type) VALUES (1, "alchemist","adventure"),(2, "wings_of_fire", "autobiography");


select * from book_bcnf_1;
select * from book_3nf_2;
select * from book_3nf_1;


joins

USE StudentDatabase;
CREATE TABLE Students (
    StudentID INT AUTO_INCREMENT PRIMARY KEY,
    FirstName VARCHAR(50),
    LastName VARCHAR(50),
    Age INT
);

create table familyinfo(
StudentID int,
Fathername varchar(50),
Mothername varchar(50),
address varchar(50),
foreign key (StudentID) references Students(StudentID)
);

select * from Students;



triggers

-- Create the student database
CREATE DATABASE StudentDatabase;
USE StudentDatabase;

-- Create a students table
CREATE TABLE Students (
    StudentID INT AUTO_INCREMENT PRIMARY KEY,
    FirstName VARCHAR(50),
    LastName VARCHAR(50),
    Age INT
);

-- Create a trigger to log student insertions
DELIMITER //
CREATE TRIGGER LogStudentInsertion
AFTER INSERT
ON Students FOR EACH ROW
BEGIN
    INSERT INTO StudentLog (StudentID, Action, Timestamp)
    VALUES (NEW.StudentID, 'INSERT', NOW());
END;
//
DELIMITER ;

-- Create a student log table to track student changes
CREATE TABLE StudentLog (
    LogID INT AUTO_INCREMENT PRIMARY KEY,
    StudentID INT,
    Action VARCHAR(10),
    Timestamp TIMESTAMP
);

insert into Students values (1,'Ankita','Dongarge',21);

select * from Students;

select * from StudentLog;


insert into Students values (2,'Prachi','Shende',14),
       (3,'Sakshi','Deshmukh',22),(4,'Shriya','patil',31); 
insert into familyinfo values(2,'Prem','Vandana','Chandrapur'),(3,'Shankar','sulbha','Sangli');

select * from familyinfo;












SELECT Students.StudentID,Students.FirstName, Students.LastName, familyinfo.Fathername, familyinfo.Mothername
FROM Students
INNER JOIN familyinfo ON Students.StudentID = familyinfo.StudentID;


SELECT Students.StudentID,Students.FirstName, Students.LastName, familyinfo.Fathername, familyinfo.Mothername
FROM Students
LEFT JOIN familyinfo ON Students.StudentID = familyinfo.StudentID;

SELECT Students.StudentID,Students.FirstName, Students.LastName, familyinfo.Fathername, familyinfo.Mothername
FROM Students
RIGHT JOIN familyinfo ON Students.StudentID = familyinfo.StudentID;


SELECT Students.StudentID,Students.FirstName, Students.LastName, familyinfo.Fathername, familyinfo.Mothername
FROM Students
LEFT JOIN familyinfo ON Students.StudentID = familyinfo.StudentID
union

SELECT Students.StudentID,Students.FirstName, Students.LastName, familyinfo.Fathername, familyinfo.Mothername
FROM Students
RIGHT JOIN familyinfo ON Students.StudentID = familyinfo.StudentID;

SELECT Students.StudentID,Students.FirstName, Students.LastName, familyinfo.Fathername, familyinfo.Mothername
FROM Students
NATURAL JOIN familyinfo ;



employees data
-- Create Employee table
-- CREATE TABLE Employee (
--     eid INT PRIMARY KEY,
--     ename VARCHAR(255),
--     address VARCHAR(255),
--     salary DECIMAL(10, 2)
-- );

-- -- Create Department table
-- CREATE TABLE Department (
--     dname VARCHAR(255) PRIMARY KEY,
--     no_of_emp INT,
--     location VARCHAR(255)
-- );

-- -- Create Worksfor table
-- CREATE TABLE Worksfor (
--     eid INT,
--     dname VARCHAR(255),
--     experience INT,
--     PRIMARY KEY (eid, dname),
--     FOREIGN KEY (eid) REFERENCES Employee(eid),
--     FOREIGN KEY (dname) REFERENCES Department(dname)
-- );

-- -- Create Project table
-- CREATE TABLE Project (
--     name VARCHAR(255) PRIMARY KEY,
--     technology VARCHAR(255),
--     duration INT
-- );

-- -- Create Emp_proj table
-- CREATE TABLE Emp_proj (
--     eid INT,
--     role VARCHAR(255),
--     name VARCHAR(255),
--     PRIMARY KEY (eid, name),
--     FOREIGN KEY (eid) REFERENCES Employee(eid),
--     FOREIGN KEY (name) REFERENCES Project(name)
-- );

-- -- Create Depends_on table
-- CREATE TABLE Depends_on (
--     eid INT,
--     name VARCHAR(255),
--     PRIMARY KEY (eid, name),
--     FOREIGN KEY (eid) REFERENCES Employee(eid),
--     FOREIGN KEY (name) REFERENCES Employee(ename)
-- );

-- Insert sample data into Employee table
INSERT INTO Employee (eid, ename, address, salary)
VALUES (1, 'John Doe', '123 Main St', 50000.00),
       (2, 'Jane Smith', '456 Elm St', 60000.00),
       (3, 'Bob Johnson', '789 Oak St', 55000.00);

-- Insert sample data into Department table
INSERT INTO Department (dname, no_of_emp, location)
VALUES ('HR', 5, 'New York'),
       ('Engineering', 20, 'San Francisco'),
       ('Sales', 10, 'Los Angeles');

-- Insert sample data into Worksfor table
INSERT INTO Worksfor (eid, dname, experience)
VALUES (1, 'HR', 2),
       (2, 'Engineering', 5),
       (3, 'Sales', 3);

-- Insert sample data into Project table
INSERT INTO Project (name, technology, duration)
VALUES ('Project A', 'Java', 12),
       ('Project B', 'Python', 9),
       ('Project C', 'C#', 15);

-- Insert sample data into Emp_proj table
INSERT INTO Emp_proj (eid, role, name)
VALUES (1, 'Manager', 'Project A'),
       (2, 'Developer', 'Project B'),
       (3, 'Sales Associate', 'Project C');

-- Insert sample data into Depends_on table
INSERT INTO Depends_on (eid, name)
VALUES (1, 'Jane Smith'),
       (2, 'Bob Johnson');
