# Experiment 3: DML Commands

## AIM
To study and implement DML (Data Manipulation Language) commands.

## THEORY

### 1. INSERT INTO
Used to add records into a relation.
These are three type of INSERT INTO queries which are as
A)Inserting a single record
**Syntax (Single Row):**
```sql
INSERT INTO table_name (field_1, field_2, ...) VALUES (value_1, value_2, ...);
```
**Syntax (Multiple Rows):**
```sql
INSERT INTO table_name (field_1, field_2, ...) VALUES
(value_1, value_2, ...),
(value_3, value_4, ...);
```
**Syntax (Insert from another table):**
```sql
INSERT INTO table_name SELECT * FROM other_table WHERE condition;
```
### 2. UPDATE
Used to modify records in a relation.
Syntax:
```sql
UPDATE table_name SET column1 = value1, column2 = value2 WHERE condition;
```
### 3. DELETE
Used to delete records from a relation.
**Syntax (All rows):**
```sql
DELETE FROM table_name;
```
**Syntax (Specific condition):**
```sql
DELETE FROM table_name WHERE condition;
```
### 4. SELECT
Used to retrieve records from a table.
**Syntax:**
```sql
SELECT column1, column2 FROM table_name WHERE condition;
```
**Question 1**
--
Decrease the reorder level by 30 percent where the product name contains 'cream' and quantity in stock is higher than reorder level in the products table.

PRODUCTS TABLE

name               type
-----------------  ---------------
product_id         INT
product_name       VARCHAR(100)
category           VARCHAR(50)
cost_price         DECIMAL(10,2)
sell_price         DECIMAL(10,2)
reorder_lvl        INT
quantity           INT
supplier_id        INT

```
update products
set reorder_lvl = reorder_lvl*0.70
where product_name like '%cream%' and quantity > reorder_lvl;

```

**Output:**

<img width="1237" height="263" alt="Screenshot 2026-08-17 113310" src="https://github.com/user-attachments/assets/82658912-d530-48b8-9631-b435039e3a6c" />


**Question 2**
---
For  Increase the selling price per unit by 3 for all products supplied by supplier ID 4 in the sales table.

PRODUCTS TABLE

name               type
-----------------  ---------------
product_id         INT
product_name       VARCHAR(100)
category           VARCHAR(50)
cost_price         DECIMAL(10,2)
sell_price         DECIMAL(10,2)
reorder_lvl        INT
quantity           INT
supplier_id        INT

SALES TABLE
name               type
-----------------  ---------------
sale_id            INT
sale_date          DATE
product_id         INT
quantity           INT
sell_price         DECIMAL(10,2)
total_sell_price   DECIMAL(10,2)

```
update sales
set sell_price=sell_price+3
where product_id in(
      select product_id
      from products
      where supplier_id=4
);


```

**Output:**

<img width="1165" height="230" alt="Screenshot 2026-08-17 113452" src="https://github.com/user-attachments/assets/bfc1836f-36fc-478b-b2fc-2bbc6b1251c0" />


**Question 3**
---
Write a SQL statement to Change the supplier name to 'A1 Suppliers' where the supplier ID is 8 in the suppliers table.

Table info

suppliers(supplier_id,supplier_name,contact_person,phone_number,email,address)

```
update suppliers
set supplier_name='A1 Suppliers'
where supplier_id=8;

```

**Output:**

<img width="1155" height="214" alt="Screenshot 2026-08-17 113704" src="https://github.com/user-attachments/assets/dcf62172-7089-4b6d-8ede-8f7beff624f6" />


**Question 4**
---
 Update the total selling price to quantity sold multiplied by updated selling price per unit where product id is 10 in the sales table.

SALES TABLE
name               type
-----------------  ---------------
sale_id            INT
sale_date          DATE
product_id         INT
quantity           INT
sell_price         DECIMAL(10,2)
total_sell_price   DECIMAL(10,2)
For example:

Test	Result
select changes();
changes()
----------
3


```
update sales 
set total_sell_price=quantity*sell_price
where product_id = 10;

```

**Output:**

<img width="1139" height="324" alt="Screenshot 2026-08-17 113928" src="https://github.com/user-attachments/assets/20a1012c-3ab4-47cf-8529-03d6145d8492" />


**Question 5**
---
Write a SQL query to Delete a Specific Surgery which was made on 28th Feb 2024.

Sample table: Surgeries

attributes: surgery_id, patient_id, surgeon_id, surgery_date

```
delete from Surgeries where surgery_date='2024-02-28'; 

```

**Output:**

<img width="874" height="271" alt="Screenshot 2026-08-17 114129" src="https://github.com/user-attachments/assets/dd6c6af1-5795-48a8-ac0b-164db7c7beda" />


**Question 6**
---
Write a SQL query to Delete All Doctors with a NULL Specialization

Sample table: Doctors

attributes : doctor_id, first_name, last_name, specialization

```
delete from Doctors where specialization is null;

```

**Output:**
<img width="1134" height="320" alt="Screenshot 2026-08-17 114227" src="https://github.com/user-attachments/assets/9650d52d-8599-4284-be6d-2bed283a82bc" />


**Question 7**
---
Write a query to get all the records from EmployeePosition table who have joined in the year 2020.

EmpID

EmpPosition

DateOfJoining

Salary

1

Manager

01/05/2024

500000

2

Executive

02/05/2024

75000

```
select * 
from EmployeePosition 
where strftime('%Y',DateOfJoining)='2020';

```

**Output:**

<img width="946" height="193" alt="Screenshot 2026-08-17 114311" src="https://github.com/user-attachments/assets/acba4f52-958a-4acd-b419-153b33c45a80" />


**Question 8**
---
Write a SQL query to determine the status of decimal in the Calculations table as 'Below Average', 'Average', or 'Above Average' based on whether it is below 50, exactly 50, or above 50.

cid         name        type        notnull     dflt_value  pk
----------  ----------  ----------  ----------  ----------  ----------
0           id          INTEGER     0                       1
1           value1      REAL        0                       0
2           value2      REAL        0                       0
3           base        INTEGER     0                       0
4           exponent    INTEGER     0                       0
5           number      REAL        0                       0
6           decimal     REAL        0                       0
 

```
select id,decimal,
  case 
     when decimal <50 then 'Below Average'
     when decimal = 50 then 'Average'
     else 'Above Average'
  End as status
from calculations;

```

**Output:**

<img width="732" height="372" alt="Screenshot 2026-08-17 114409" src="https://github.com/user-attachments/assets/e46973bf-a3bd-4d91-bdbf-df72b9ef089c" />


**Question 9**
---
Write a SQL query to find the details of those salespeople who live in cities other than Paris and Rome. Return salesman_id, name, city, commission.

Sample table: salesman

 salesman_id |    name    |   city   | commission 
-------------+------------+----------+------------
        5001 | James Hoog | New York |       0.15
        5002 | Nail Knite | Paris    |       0.13
        5005 | Pit Alex   | London   |       0.11

```
select * from salesman where city not in ('Paris', 'Rome');

```

**Output:**
<img width="894" height="285" alt="Screenshot 2026-08-17 114452" src="https://github.com/user-attachments/assets/41b91002-6cf8-492d-a516-9610ec6fc714" />


**Question 10**
---
Write a SQL query to round the decimal column to 3 decimal places from the Calculations table.

cid         name        type        notnull     dflt_value  pk
----------  ----------  ----------  ----------  ----------  ----------
0           id          INTEGER     0                       1
1           value1      REAL        0                       0
2           value2      REAL        0                       0
3           base        INTEGER     0                       0
4           exponent    INTEGER     0                       0
5           number      REAL        0                       0
6           decimal     REAL        0                       0
 

```
select id, ROUND(decimal, 3) as rounded_value
from Calculations;

```

**Output:**

<img width="528" height="200" alt="Screenshot 2026-08-17 114544" src="https://github.com/user-attachments/assets/563ccf3c-a494-4dd0-b3bb-a786d58d9001" />


## RESULT
Thus, the SQL queries to implement DML commands have been executed successfully.
