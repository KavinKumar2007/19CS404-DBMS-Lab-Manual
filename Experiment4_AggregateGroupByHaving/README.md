# Experiment 4: Aggregate Functions, Group By and Having Clause

## AIM
To study and implement aggregate functions, GROUP BY, and HAVING clause with suitable examples.

## THEORY

### Aggregate Functions
These perform calculations on a set of values and return a single value.

- **MIN()** – Smallest value  
- **MAX()** – Largest value  
- **COUNT()** – Number of rows  
- **SUM()** – Total of values  
- **AVG()** – Average of values

**Syntax:**
```sql
SELECT AGG_FUNC(column_name) FROM table_name WHERE condition;
```
### GROUP BY
Groups records with the same values in specified columns.
**Syntax:**
```sql
SELECT column_name, AGG_FUNC(column_name)
FROM table_name
GROUP BY column_name;
```
### HAVING
Filters the grouped records based on aggregate conditions.
**Syntax:**
```sql
SELECT column_name, AGG_FUNC(column_name)
FROM table_name
GROUP BY column_name
HAVING condition;
```

**Question 1**
--
What is the average duration of insurance coverage for patients covered by each insurance company?

Sample table:Insurance Table

name               type
-----------------  ----------
InsuranceID        INTEGER
PatientID          INTEGER
InsuranceCompany   TEXT
PolicyNumber       TEXT
PolicyHolder       TEXT
StartDate          DATE
EndDate            DATE
For example:

Result
InsuranceCompany  AvgCoverageDurationDays
----------------  -----------------------
ABC Insurance     7.0
DEF Insurance     3.0
JKL Insurance     3.0
STU Insurance     3.0
VWX Insurance     3.0
XYZ Insurance     3.0
YZA Insurance     3.0

```
select InsuranceCompany,avg(EndDate - StartDate) as AvgCoverageDurationDays from Insurance group by InsuranceCompany  

```

**Output:**

<img width="787" height="552" alt="Screenshot 2026-08-28 204220" src="https://github.com/user-attachments/assets/c733cd86-bb63-4d0e-8511-2b9b7988f2f8" />


**Question 2**
---
Write a SQL query to find the total number of unique cities in the customer table?

Table: customer

name        type
----------  ----------
id          INTEGER
name        TEXT
city        TEXT
email       TEXT
phone       INTEGER
For example:

Result
unique_cities
-------------
10


```

select count(distinct(city)) as unique_cities from customer

```

**Output:**

<img width="333" height="207" alt="Screenshot 2026-08-28 204407" src="https://github.com/user-attachments/assets/d259c147-db42-4663-aaed-434efaf10d7b" />


**Question 3**
---

Write a SQL query to find how many employees have an income greater than 50K?

Table: employee

name        type
----------  ----------
id          INTEGER
name        TEXT
age         INTEGER
city        TEXT
income      INTEGER
For example:

Result
employees_count
---------------
8


```
select count(income) as employees_count from employee where income > 50000

```

**Output:**

<img width="376" height="212" alt="Screenshot 2026-08-28 204520" src="https://github.com/user-attachments/assets/2300a013-1311-4ff2-9278-e04d0fb82901" />


**Question 4**
---
Write a SQL query to find the shortest email address in the customer table?

Table: customer

name        type
----------  ----------
id          INTEGER
name        TEXT   
city        TEXT
email       TEXT
phone       INTEGER
For example:

Result
name        email           min_email_length
----------  --------------  ----------------
Ravi Kumar  ravi@gmail.com  14


```
select name,email,min(length(email)) as min_email_length from customer 

```

**Output:**

<img width="886" height="210" alt="Screenshot 2026-08-28 204612" src="https://github.com/user-attachments/assets/28a7652d-75e7-4dbe-9450-066093bf4558" />


**Question 5**
---
Write a SQL query to find the youngest employee in the company?

Table: employee

name        type
----------  ----------
id          INTEGER
name        TEXT
age         INTEGER
city        TEXT
income      INTEGER
 

For example:

Result
Employee_Name  Age
-------------  ----------
Peter          32


```
select name as Employee_Name,min(age) as Age from employee 

```

**Output:**

<img width="538" height="221" alt="Screenshot 2026-08-28 204706" src="https://github.com/user-attachments/assets/388627b5-ef56-4cab-8594-fd5d113f5ecd" />


**Question 6**
---
How many patients have insurance coverage valid in each year?

Sample table:Insurance Table

name               type
-----------------  ----------
InsuranceID        INTEGER
PatientID          INTEGER
InsuranceCompany   TEXT
PolicyNumber       TEXT
PolicyHolder       TEXT
ValidityPeriod     TEXT
For example:

Result
ValidityYear  TotalPatients
------------  -------------
2024          3
2025          1
2027          4
2031          2


```
SELECT 
    SUBSTR(ValidityPeriod, 1, 4) AS ValidityYear,
    COUNT(DISTINCT PatientID) AS TotalPatients
FROM Insurance
GROUP BY SUBSTR(ValidityPeriod, 1, 4);

```

**Output:**

<img width="571" height="287" alt="Screenshot 2026-08-28 204846" src="https://github.com/user-attachments/assets/b1cdee52-56c9-48d6-9eb1-1816c4454147" />


**Question 7**
---
Write a SQL query to find What is the age difference between the youngest and oldest employee in the company.

Table: employee

name        type
----------  ----------
id          INTEGER
name        TEXT
age         INTEGER
city        TEXT
income      INTEGER
For example:

Result
age_difference
--------------
13


```
SELECT MAX(age) - MIN(age) AS age_difference
FROM employee;

```

**Output:**

<img width="352" height="210" alt="Screenshot 2026-08-28 204936" src="https://github.com/user-attachments/assets/2aebfd36-ef39-4ec9-bc3a-c47cdd6b0838" />


**Question 8**
---
Write a SQL query to find the average length of email addresses (in characters):

Table: customer

name        type
----------  ----------
id          INTEGER
name        TEXT
city        TEXT
email       TEXT
phone       INTEGER
For example:

Result
avg_email_length
----------------
15.0


```
SELECT AVG(LENGTH(email)) AS avg_email_length
FROM customer;

```

**Output:**

<img width="392" height="220" alt="Screenshot 2026-08-28 205015" src="https://github.com/user-attachments/assets/80828d0d-8cf8-40a4-bc83-10fb7281a078" />


**Question 9**
---
Write a SQL query to find the difference between the maximum and minimum price of fruits?

Table: fruits

name        type
----------  ----------
id          INTEGER
name        TEXT
unit        TEXT
inventory   INTEGER
price       REAL
 

For example:

Result
price_diff
----------
4.65


```
SELECT MAX(price) - MIN(price) AS price_diff
FROM fruits;

```

**Output:**

<img width="325" height="228" alt="Screenshot 2026-08-28 205108" src="https://github.com/user-attachments/assets/2b61dc24-10e8-421c-8494-9162f0aa293d" />


**Question 10**
---
Write a SQL query to find the customer with longest name?

Table: customer

name        type
----------  ----------
id          INTEGER
name        TEXT
city        TEXT
email       TEXT
phone       INTEGER
For example:

Result
name          length
------------  ----------
Preeti Patel  12


```
SELECT name, LENGTH(name) AS length
FROM customer
ORDER BY LENGTH(name) DESC
LIMIT 1;
```

**Output:**

<img width="572" height="233" alt="Screenshot 2026-08-28 210026" src="https://github.com/user-attachments/assets/4cc72e67-0fba-4b48-99c3-74000a68068a" />



## RESULT
Thus, the SQL queries to implement aggregate functions, GROUP BY, and HAVING clause have been executed successfully.
