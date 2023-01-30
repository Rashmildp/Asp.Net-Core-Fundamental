# SQL Short Note 💚🛸
```bash
create table student (
student_id int ,
name varchar(50),
major varchar (50)
);

```
```bash
insert into student values (1,'Rashmi','IT');

```
Drop table
```bash
drop table student;
```
Alter keyword
```bash
Alter table student add gpa decimal(3,2);
Alter table student drop column gpa;
```
Constraints
```bash
  Create table student(
   student_id int auto_increment,
   name varchar(50) not null,
   major varchar (50) Default 'UNDECIDED',
   primary key (student_id)
  );
```
Update
```bash
update student set major= 'BIO'
where major = 'Biology';
```
Delete
```bash
Delete from student 
where student_id=2;
```
Basic Queries
```bash
select student.id , student.name
from student
order by name DESC
```
Retrive specific number of rows
```bash
select *
from student
limit 2;
```
Not Equal
```bash
<>
```
In keyword
```bash
select *
from student
where name IN ('RAS', 'KATR', 'PETER');
```
Foreign key
```bash
craete table branch (
branch_id int primary key,
name varchar (50),
mgr_id int,
mgr_startDate DATE,
Foreign key (mgr_id) REFERENCES employee(emp_id) ON DELETE SET NULL
);
```
Find all employee order by salary
```bash
select *
from employee
order by salary DESC
```
As keyword
```bash
select first_Name as forname
```
Find out all different genders (Distinct keyword)
```bash
select Distinct sex
from employee
```
**Functions**

Find the number of employees
```bash
select count(emp_id)
from employee
```
Find the number of female employees
```bash
select count(emp_id)
from employee
where sex= 'F'
```
Find the average of all employees salary
```bash
select avg(salary)
from employee
// SUM , MIN , MAX

```

Find howmany males and females
```bash
select count(sex), sex
from employee
group by sex
```
Find the total sales of each employee
```bash
select sum(total_sales) , emp_id
from employee
group by emp_id;
```

**Wildcard**

Used to defining patterns to match specific requirements.

Find any clients who are LLC
```bash
select *
from employee
where client_name like '%LLC'
```
Find any employee born in october
```bash
select *
from employee 
where birth_date like '____-10%';
// _ represents in one character
```
**UNION**

Combine results from multiple select statements

Find the list of employee names and branch name
```bash
select first_Name
from employee
UNION
select branch_name
from branch
```
**JOIN**

Joins are used to Combine rows from different tables based on a retaled column and useful for combining information from different tables into one single table.

**Inner Join**

Combine only employee id equal to manager id

(shared columns are common)

```bash
select 
from employee
join branch
on employee.emp_id = branch.mgr_id
```

**Left Join**

All of the employess table include in the results and but only the rows in the branch table that matched. (branch table is the right table)

```bash
select
from employee
left join branch
on employee.emp_id = branch.mgr_id
```
**Right Join**

All the rows from branch included in the final result. 

select
from employee
right join branch
on employee.emp_id = branch.mgr_id

**Outer Join**

All of the rows from employee table and all rows from branch table include in the final result.

```bash
select 
from employee
outer join branch
on employee.emp_id = branch.mgr_id
```

**Nested Queries**

Find all employees who have who have sold over 30000 to a single client

```bash
select employee.first_Name , employee.last_Name
from employee
where employee.emp_id IN (
         select works_with.emp_id
         from works_with
         where works_with.total > 30000;
        );

```

Find all clinets who are handled by the branch that Micheal Scott manages

```bash
// find the Branch id which handles by 


select client.client_id
from client
where client.branch_id IN (
   
           select branch.branch_id
           from branch
            where branch.mgr_id = (
            select employee.emp_id
            from employee 
             where employee.first_Name = 'Micheal' AND employee.   last_Name='Scott'
)
)

```
**ON DELETE**
1. On delete cascade

when manager is deleted in the table and associate table (Branch) , mgr_id set to null. 

```bash
Foreign key (mgr_id) REFERENCES employee (emp_id) on delete set NUll

```

Which means if the employee id from the employeetable gets deleted , set the branch mgr_id as NULL. 


2. On delete cascade (use when Foreign key is part of the primary key) 

If delete branch 2 , all of the rows that have branch id in this table would be deleted. 

**Triggers**

Triggers are basically a block of code which can define a certain action should happen .
```bash
craete trigger myTrigger Before insert
on Employee
for each row begin
insert into myTrigger values ("Added new employee");

```
