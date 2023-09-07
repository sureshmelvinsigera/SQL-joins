# SQL Joins

## Example 1

Here are two SQL tables, `Student` and `Language`, along with some sample data. We'll then provide examples of left join, right join, inner join, and full join using these tables.

```SQL
-- Create the User table
CREATE TABLE Student (
    student_id INT PRIMARY KEY,
    name VARCHAR(50),
    age INT
);

-- Insert sample data into the User table
INSERT INTO Student (student_id, name, age)
VALUES
    (1, 'Alice', 28),
    (2, 'Bob', 35),
    (3, 'Charlie', 22),
    (4, 'David', 30);

-- Create the Language table
CREATE TABLE Language (
    language_id INT PRIMARY KEY,
    student_id INT,
    name VARCHAR(50)
);

-- Insert sample data into the Language table
INSERT INTO Language (language_id, student_id, name)
VALUES
    (1, 1, 'English'),
    (2, 1, 'Spanish'),
    (3, 2, 'French'),
    (4, 3, 'German'),
    (5, 4, 'Chinese');
```

Now that we have the tables and data set up, let's provide examples of different types of joins:

**Left Join**: Returns all rows from the left table (`Student`) and the matching rows from the right table (`Language`). If there's no match, `NULL` values are returned for columns from the right table.

```SQL
SELECT Student.name, Student.age, Language.name
FROM Student
LEFT JOIN Language ON Student.student_id = Language.student_id;
```

<img width="397" alt="image" src="https://github.com/sureshmelvinsigera/SQL-joins/assets/20378525/bfad6d03-9391-4a31-9e6e-505b6efbe037">

**Right Join**: Returns all rows from the right table (`Language`) and the matching rows from the left table (`Student`). If there's no match, `NULL` values are returned for columns from the left table.

```SQL
SELECT Student.name, Student.age, Language.name
FROM Student
RIGHT JOIN Language ON Student.student_id = Language.student_id;
```

<img width="395" alt="image" src="https://github.com/sureshmelvinsigera/SQL-joins/assets/20378525/26e25c1e-b19f-46e9-b3e6-ebe533ba9457">

**Inner Join**: Returns only the rows with matching values in both tables (`Student` and `Language`).

```SQL
SELECT Student.name, Student.age, Language.name
FROM Student
INNER JOIN Language ON Student.student_id = Language.student_id;
```

<img width="394" alt="image" src="https://github.com/sureshmelvinsigera/SQL-joins/assets/20378525/0035d40d-40da-4dc0-9dc0-ed1f025d2eb8">

**Full Join (Not supported in all database systems)**: Returns all rows when there is a match in either the left table (`User`) or the right table (`Language`). It includes all rows from both tables and fills in `NULL` values when there's no match.

```SQL
SELECT Student.name, Student.age, Language.name
FROM Student
FULL JOIN Language ON Student.student_id = Language.student_id;
```

<img width="396" alt="image" src="https://github.com/sureshmelvinsigera/SQL-joins/assets/20378525/b4fd0d94-1413-4185-b759-4003044b3089">

Please note that the availability of `FULL JOIN` may vary depending on the specific database system you are using. Some database systems, like MySQL, do not support `FULL JOIN`, and you may need to use a combination of `LEFT JOIN` and `RIGHT JOIN` to achieve similar results.

<hr>

## Example 2

```SQL
-- Create the Employees table
CREATE TABLE Employees (
    EmployeeID INT PRIMARY KEY,
    FirstName VARCHAR(50),
    LastName VARCHAR(50),
    DepartmentID INT
);

-- Insert sample data into the Employees table
INSERT INTO Employees (EmployeeID, FirstName, LastName, DepartmentID)
VALUES
    (1, 'Alice', 'Smith', 101),
    (2, 'Bob', 'Johnson', 102),
    (3, 'Charlie', 'Brown', 103),
    (4, 'David', 'Lee', 101),
    (5, 'Eve', 'Taylor', NULL);

-- Create the Departments table
CREATE TABLE Departments (
    DepartmentID INT PRIMARY KEY,
    DepartmentName VARCHAR(50)
);

-- Insert sample data into the Departments table
INSERT INTO Departments (DepartmentID, DepartmentName)
VALUES
    (101, 'Sales'),
    (102, 'Marketing'),
    (103, 'Finance'),
    (104, 'HR');
```

Now that we have the tables and data set up, let's provide examples of each type of join:

**LEFT JOIN**: Returns all rows from the left table (`Employees`) and the matching rows from the right table (`Departments`). If there's no match, `NULL` values are returned for columns from the right table.

```SQL
SELECT Employees.FirstName, Employees.LastName, Departments.DepartmentName
FROM Employees
LEFT JOIN Departments ON Employees.DepartmentID = Departments.DepartmentID;
```

FirstName   | LastName | DepartmentName
------------|----------|----------------
Alice       | Smith    | Sales
Bob         | Johnson  | Marketing
Charlie     | Brown    | Finance
David       | Lee      | Sales
Eve         | Taylor   | NULL


**RIGHT JOIN**: Returns all rows from the right table (`Departments`) and the matching rows from the left table (`Employees`). If there's no match, `NULL` values are returned for columns from the left table.

```SQL
SELECT Employees.FirstName, Employees.LastName, Departments.DepartmentName
FROM Employees
RIGHT JOIN Departments ON Employees.DepartmentID = Departments.DepartmentID;
```

FirstName   | LastName | DepartmentName
------------|----------|----------------
Alice       | Smith    | Sales
Bob         | Johnson  | Marketing
Charlie     | Brown    | Finance
NULL        | NULL     | HR


**INNER JOIN**: Returns only the rows with matching values in both tables (`Employees` and `Departments`).

```SQL
SELECT Employees.FirstName, Employees.LastName, Departments.DepartmentName
FROM Employees
INNER JOIN Departments ON Employees.DepartmentID = Departments.DepartmentID;
```

FirstName   | LastName | DepartmentName
------------|----------|----------------
Alice       | Smith    | Sales
Bob         | Johnson  | Marketing
Charlie     | Brown    | Finance
David       | Lee      | Sales


**FULL JOIN (Simulated using UNION ALL)**: Returns all rows when there is a match in either the left table (`Employees`) or the right table (`Departments`). It includes all rows from both tables and fills in `NULL` values when there's no match. Note that not all database systems support `FULL JOIN`, so we simulate it using `UNION ALL`.

```
SELECT Employees.FirstName, Employees.LastName, Departments.DepartmentName
FROM Employees
LEFT JOIN Departments ON Employees.DepartmentID = Departments.DepartmentID
UNION ALL
SELECT Employees.FirstName, Employees.LastName, Departments.DepartmentName
FROM Employees
RIGHT JOIN Departments ON Employees.DepartmentID = Departments.DepartmentID;
```

FirstName   | LastName | DepartmentName
------------|----------|----------------
Alice       | Smith    | Sales
Bob         | Johnson  | Marketing
Charlie     | Brown    | Finance
David       | Lee      | Sales
NULL        | NULL     | HR


This example demonstrates the behavior of each type of join using the `Employees` and `Departments` tables and provides you with an understanding of how they work
