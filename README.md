# sql-practice

## SQL Practice №2 | Employee management

#### Relational scheme

![](https://user-images.githubusercontent.com/69513400/130349636-c78c7f41-8215-4326-8c23-5eee7f11ebbd.png)


#### Table creation code

``` sql
  CREATE TABLE Departments (
     Code INTEGER PRIMARY KEY NOT NULL,
     Name NVARCHAR NOT NULL ,
     Budget REAL NOT NULL 
   );

   CREATE TABLE Employees (
     SSN INTEGER PRIMARY KEY NOT NULL,
     Name TEXT NOT NULL ,
     LastName VARCHAR NOT NULL ,
     Department INTEGER NOT NULL , 
     CONSTRAINT fk_Departments_Code FOREIGN KEY(Department) 
     REFERENCES Departments(Code)
   );
```

#### Sample dataset

``` sql
INSERT INTO Departments (Code, Name, Budget) VALUES (14, 'IT', 65000);
INSERT INTO Departments (Code, Name, Budget) VALUES (37, 'Accounting', 15000);
INSERT INTO Departments (Code, Name, Budget) VALUES (59, 'Human Resources', 240000);
INSERT INTO Departments (Code, Name, Budget) VALUES (77, 'Research', 55000);

INSERT INTO Employees (SSN, Name, LastName, Department) VALUES ('123234877', 'Michael', 'Rogers', 14);
INSERT INTO Employees (SSN, Name, LastName, Department) VALUES ('152934485', 'Anand', 'Manikutty', 14);
INSERT INTO Employees (SSN, Name, LastName, Department) VALUES ('222364883', 'Carol', 'Smith', 37);
INSERT INTO Employees (SSN, Name, LastName, Department) VALUES ('326587417', 'Joe', 'Stevens', 37);
INSERT INTO Employees (SSN, Name, LastName, Department) VALUES ('332154719', 'Mary-Anne', 'Foster', 14);
INSERT INTO Employees (SSN, Name, LastName, Department) VALUES ('332569843', 'George', 'O''Donnell', 77);
INSERT INTO Employees (SSN, Name, LastName, Department) VALUES ('546523478', 'John', 'Doe', 59);
INSERT INTO Employees (SSN, Name, LastName, Department) VALUES ('631231482', 'David', 'Smith', 77);
INSERT INTO Employees (SSN, Name, LastName, Department) VALUES ('654873219', 'Zacary', 'Efron', 59);
INSERT INTO Employees (SSN, Name, LastName, Department) VALUES ('745685214', 'Eric', 'Goldsmith', 59);
INSERT INTO Employees (SSN, Name, LastName, Department) VALUES ('845657245', 'Elizabeth', 'Doe', 14);
INSERT INTO Employees (SSN, Name, LastName, Department) VALUES ('845657246', 'Kumar', 'Swamy', 14);
```

#### Exercises

1. Select the last name of all employees.
2. Select the last name of all employees, without duplicates.
3. Select all the data of employees whose last name is "Smith".
4. Select all the data of employees whose last name is "Smith" or "Doe".
5. Select all the data of employees that work in department 14.
6. Select all the data of employees that work in department 37 or department 77.
7. Select all the data of employees whose last name begins with an "S".
8. Select the sum of all the departments' budgets.
9. Select the number of employees in each department (you only need to show the department code and the number of employees).
10. Select all the data of employees, including each employee's department's data.
11. Select the name and last name of each employee, along with the name and budget of the employee's department.
12. Select the name and last name of employees working for departments with a budget greater than $60,000.
13. Select the departments with a budget larger than the average budget of all the departments.
14. Select the names of departments with more than two employees.
15. Select the name and last name of employees working for departments with second lowest budget.
16. Add a new department called "Quality Assurance", with a budget of $40,000 and departmental code 11. Add an employee called "Mary Moore" in that department, with SSN 847-21-9811.
17. Reduce the budget of all departments by 10%.
18. Reassign all employees from the Research department (code 77) to the IT department (code 14).
19. Delete from the table all employees in the IT department (code 14).
20. Delete from the table all employees who work in departments with a budget greater than or equal to $60,000.
21. Delete from the table all employees.

#### Answers

``` sql
  SELECT lastname FROM employees;
  SELECT DISTINCT lastname FROM employees;
  SELECT * FROM employees WHERE lastname = 'Smith';
  SELECT * FROM employees WHERE lastname IN ('Smith', 'Doe');
  SELECT * FROM employees WHERE department = 14;
  SELECT * FROM employees WHERE department IN (37, 77);
  SELECT * FROM employees WHERE lastname LIKE 'S%';
  SELECT sum(budget) FROM departments;
  SELECT department, count(*) FROM Employees GROUP BY department;
  SELECT * FROM employees e JOIN departments d ON d.code = e.department;
  SELECT e.name, e.lastname, d.name, d.budget FROM employees e JOIN departments d ON d.code = e.department; 
  SELECT e.name, e.lastname FROM employees e JOIN departments d ON d.code = e.department WHERE d.budget > 60000;
  SELECT * FROM Departments WHERE budget > (SELECT avg(budget) FROM departments);
  SELECT d.name FROM departments d JOIN employees e ON e.department = d.code GROUP BY d.code HAVING count(e) > 2;
  SELECT e.name, e.lastname FROM employees e JOIN departments d ON d.code = e.department WHERE budget = 55000;
  INSERT INTO departments(code, name, budget) VALUES (11,'Quality Assurance',40000);
  INSERT INTO employees (ssn, name, lastname, department) VALUES (847219811, 'Mary', 'Moore', 11);
  UPDATE departments SET budget = budget * 0.9;
  UPDATE employees SET department = 14 WHERE department = 77;
  DELETE FROM employees WHERE department = 14;
  DELETE FROM employees WHERE department IN (SELECT code FROM departments WHERE budget >= 60000)
  DELETE FROM employees;
```
