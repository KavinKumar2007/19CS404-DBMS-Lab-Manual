# Experiment 2: DDL Commands

## AIM
To study and implement DDL commands and different types of constraints.

## THEORY

### 1. CREATE
Used to create a new relation (table).

**Syntax:**
```sql
CREATE TABLE (
  field_1 data_type(size),
  field_2 data_type(size),
  ...
);
```
### 2. ALTER
Used to add, modify, drop, or rename fields in an existing relation.
(a) ADD
```sql
ALTER TABLE std ADD (Address CHAR(10));
```
(b) MODIFY
```sql
ALTER TABLE relation_name MODIFY (field_1 new_data_type(size));
```
(c) DROP
```sql
ALTER TABLE relation_name DROP COLUMN field_name;
```
(d) RENAME
```sql
ALTER TABLE relation_name RENAME COLUMN old_field_name TO new_field_name;
```
### 3. DROP TABLE
Used to permanently delete the structure and data of a table.
```sql
DROP TABLE relation_name;
```
### 4. RENAME
Used to rename an existing database object.
```sql
RENAME TABLE old_relation_name TO new_relation_name;
```
### CONSTRAINTS
Constraints are used to specify rules for the data in a table. If there is any violation between the constraint and the data action, the action is aborted by the constraint. It can be specified when the table is created (using CREATE TABLE) or after it is created (using ALTER TABLE).
### 1. NOT NULL
When a column is defined as NOT NULL, it becomes mandatory to enter a value in that column.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) NOT NULL
);
```
### 2. UNIQUE
Ensures that values in a column are unique.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) UNIQUE
);
```
### 3. CHECK
Specifies a condition that each row must satisfy.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) CHECK (logical_expression)
);
```
### 4. PRIMARY KEY
Used to uniquely identify each record in a table.
Properties:
Must contain unique values.
Cannot be null.
Should contain minimal fields.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) PRIMARY KEY
);
```
### 5. FOREIGN KEY
Used to reference the primary key of another table.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size),
  FOREIGN KEY (column_name) REFERENCES other_table(column)
);
```
### 6. DEFAULT
Used to insert a default value into a column if no value is specified.

Syntax:
```sql
CREATE TABLE Table_Name (
  col_name1 data_type,
  col_name2 data_type,
  col_name3 data_type DEFAULT 'default_value'
);
```

**Question 1**
--
  Create a table named Products with the following constraints:
  ProductID as INTEGER should be the primary key.
  ProductName as TEXT should be unique and not NULL.
  Price as REAL should be greater than 0.
  StockQuantity as INTEGER should be non-negative.

```
create table Products(
ProductID integer primary key,
ProductName text unique not null,
Price real check(Price>0),
StockQuantity integer check(StockQuantity>0)
)
```

**Output:**

<img width="1072" height="207" alt="Screenshot 2026-08-17 104811" src="https://github.com/user-attachments/assets/f41bc3a1-bf86-4dbc-9db8-5f4cf5aa3cc8" />


**Question 2**
---
Create a table named Orders with the following constraints:
OrderID as INTEGER should be the primary key.
OrderDate as DATE should be not NULL.
CustomerID as INTEGER should be a foreign key referencing Customers(CustomerID).

```
create table Orders(
OrderID integer primary key,
OrderDate date not null,
CustomerID integer,
foreign key(CustomerID) references Customers(CustomerID)
)

```

**Output:**

<img width="733" height="191" alt="Screenshot 2026-08-17 105027" src="https://github.com/user-attachments/assets/cab9382b-949b-4d07-85c6-17e07b32c27b" />


**Question 3**
---
Insert all products from Discontinued_products into Products.

Table attributes are ProductID, ProductName, Price, Stock

```
insert into Products select * from Discontinued_products

```

**Output:**

<img width="988" height="210" alt="Screenshot 2026-08-17 105254" src="https://github.com/user-attachments/assets/64e75a5f-a21d-448e-b881-51d16e5ed48b" />


**Question 4**
---
Insert the below data into the Books table, allowing the Publisher and Year columns to take their default values.

ISBN             Title                 Author
---------------  --------------------  ---------------
978-6655443321   Big Data Analytics    Karen Adams

Note: The Publisher and Year columns will use their default values.
```
insert into Books(ISBN,Title,Author) values ('978-6655443321','Big Data Analytics','Karen Adams')

```

**Output:**

<img width="1063" height="239" alt="Screenshot 2026-08-17 105431" src="https://github.com/user-attachments/assets/ee1238f5-81b0-487e-95a0-7b6d37400136" />


**Question 5**
---
In the Books table, insert a record where some fields are NULL, another record where all fields are filled without any NULL values, and a third record where some fields are filled, and others are left as NULL.

ISBN             Title                      Author           Publisher   Year
---------------  -------------------------  ---------------  ----------  ----------
978-1234567890   Introduction to AI         John Doe
978-9876543210   Deep Learning              Jane Doe         TechPress   2022
978-1122334455   Cybersecurity Essentials   Alice Smith                  2021

```
insert into Books(ISBN,Title,Author,Publisher,Year) values ('978-1234567890','Introduction to AI' ,'John Doe'," "," "), 
                                                            ('978-9876543210','Deep Learning','Jane Doe','TechPress','2022'),
                                                            ('978-1122334455','Cybersecurity Essentials','Alice Smith'," ",'2021')

```

**Output:**
<img width="1053" height="135" alt="Screenshot 2026-08-17 105737" src="https://github.com/user-attachments/assets/418cc39e-f91e-4b51-9024-2b1b19f5a336" />

**Question 6**
---
create a table named jobs including columns job_id, job_title, min_salary and max_salary, and make sure that, the default value for job_title is blank and min_salary is 8000 and max_salary is NULL will be entered automatically at the time of insertion if no value assigned for the specified columns.

```
create table jobs (
job_id integer primary key,
job_title text default " ",
min_salary integer default 8000,
max_salary integer default null
)

```

**Output:**

<img width="1043" height="231" alt="Screenshot 2026-08-17 105843" src="https://github.com/user-attachments/assets/371aaed9-5db1-41e6-a545-249adcf4326b" />


**Question 7**
---
Write a SQL query to Add a new column State as text in the Student_details table.

Sample table: Student_details

 cid              name             type   notnull     dflt_value  pk
---------------  ---------------  -----  ----------  ----------  ----------
0                RollNo           int    0                       1
1                Name             VARCH  1                       0
2                Gender           TEXT   1                       0
3                Subject          VARCH  0                       0
4                MARKS            INT (  0                       0

```
alter table Student_details 
add column State TEXT

```

**Output:**

<img width="1198" height="252" alt="Screenshot 2026-08-17 110213" src="https://github.com/user-attachments/assets/0da098a4-6d56-4b9b-8775-48d77494a379" />


**Question 8**
---
Create a table named Employees with the following columns:

EmployeeID as INTEGER
FirstName as TEXT
LastName as TEXT
HireDate as DATE

``` 
create table Employees(
EmployeeID INTEGER,
FirstName TEXT,
LastName TEXT,
HireDate DATE
)

```

**Output:**

<img width="1156" height="233" alt="Screenshot 2026-08-17 110452" src="https://github.com/user-attachments/assets/0bb826f1-c0f4-4acc-b689-c8a012b1fc2f" />


**Question 9**
---
Write a SQL query to modify the Student_details table by adding a new column Email of type VARCHAR(50) and updating the column MARKS to have a default value of 0.

```
alter table student_details
add column Email varchar(50);
alter table student_details
add column MARKS  default 0

```

**Output:**

<img width="1213" height="129" alt="Screenshot 2026-08-17 110736" src="https://github.com/user-attachments/assets/c1c5c798-9918-4cdc-9558-a2128e471233" />


**Question 10**
---
Create a table named Invoices with the following constraints:
InvoiceID as INTEGER should be the primary key.
InvoiceDate as DATE.
Amount as REAL should be greater than 0.
DueDate as DATE should be greater than the InvoiceDate.
OrderID as INTEGER should be a foreign key referencing Orders(OrderID).

```
create table Invoices(
InvoiceID integer primary key,
InvoiceDate date,
Amount real check(Amount>0),
DueDate date check(DueDate > InvoiceDate),
OrderID integer,
foreign key(OrderID) references Orders(OrderID)
)

```

**Output:**
<img width="1041" height="183" alt="Screenshot 2026-08-17 110842" src="https://github.com/user-attachments/assets/2831dd44-b465-472d-b57e-511026f30e4f" />



## RESULT
Thus, the SQL queries to implement different types of constraints and DDL commands have been executed successfully.
