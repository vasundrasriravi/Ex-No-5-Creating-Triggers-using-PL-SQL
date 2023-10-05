# Ex. No: 5 Creating Triggers using PL/SQL

### AIM: 
To create a Trigger using PL/SQL.

### Steps:
1. Create employee table with following attributes (empid NUMBER, empname VARCHAR(10), dept VARCHAR(10),salary NUMBER);
2. Create salary_log table with following attributes (log_id NUMBER GENERATED ALWAYS AS IDENTITY, empid NUMBER,empname VARCHAR(10),old_salary NUMBER,new_salary NUMBER,update_date DATE);
3. Create a trigger named as log_salary-update.
4. Inside the trigger block, Insert the values into the salary_log table whenever the salary is updated.
5. End the trigger.
6. Update the salary of an employee in employee table.
7. Whenever a salary is updated for the employee it must be logged into the salary_log table with old salary and new salary.
8. Display the employee table, salary_log table.

### Program:
### Create employee table
```
SQL> create table EmployeeNew(Empno NUMBER,Empname VARCHAR2(10),Dept VARCHAR2(10),Desig VARCHAR2(20),Salary NUMBER);
```
![sql1](https://github.com/vasundrasriravi/Ex-No-5-Creating-Triggers-using-PL-SQL/assets/119393983/d6766990-bc44-461e-9138-aa975dc265f4)

### Create salary_log table
```
SQL> create table Sal_Wages(Empno NUMBER,Empname VARCHAR2(10),Old_Salary NUMBER,New_Salary NUMBER,Updated_on DATE);
```
![sql2](https://github.com/vasundrasriravi/Ex-No-5-Creating-Triggers-using-PL-SQL/assets/119393983/7f62c736-d82b-4cf9-a754-b7781a590b8d)

### inserting data into the employed table:
```
SQL> insert into EmployeeNew values(101,'vasundra','AI-DS','Senior Architect',500000);
SQL> insert into EmployeeNew values(102,'deepii','cyber','System engineer',400000);
SQL> insert into EmployeeNew values(103,'Abinaya','CSE','Software Tester',230000);
SQL> insert into EmployeeNew values(104,'surya','AIML','Developer',270000);
SQL> insert into EmployeeNew values(105,'Diana','IT','Analysist',600000);
```
![sql3](https://github.com/vasundrasriravi/Ex-No-5-Creating-Triggers-using-PL-SQL/assets/119393983/40c5b8db-c416-490a-8ffb-ca59436ba9f7)
![sql3 1](https://github.com/vasundrasriravi/Ex-No-5-Creating-Triggers-using-PL-SQL/assets/119393983/cb701c95-25b9-4bbd-8fc2-0a36f343f9ec)

### update the salary of an employed:
```
SQL> update EmployeeNew SET Salary=100000 where Empno=103;
```
![sql4](https://github.com/vasundrasriravi/Ex-No-5-Creating-Triggers-using-PL-SQL/assets/119393983/aec603e6-31cf-4645-b3a9-21a92cb7ff84)

### PLSQL Trigger code
```
SQL> CREATE OR REPLACE TRIGGER Salary_Update
  2  BEFORE UPDATE ON EmployeeNew
  3  FOR EACH ROW
  4  BEGIN
  5  IF :OLD.Salary != :NEW.Salary THEN
  6  INSERT INTO Sal_Wages (Empno, Empname, Old_Salary, New_Salary, Updated_on)
  7  VALUES (:OLD.Empno, :OLD.Empname, :OLD.Salary, :NEW.Salary, SYSDATE);
  8  END IF;
  9  END;
 10  /
```
![sql5](https://github.com/vasundrasriravi/Ex-No-5-Creating-Triggers-using-PL-SQL/assets/119393983/34a3e61d-4acd-4f35-bdb9-40d2eda0e039)

### Output:
![sql6](https://github.com/vasundrasriravi/Ex-No-5-Creating-Triggers-using-PL-SQL/assets/119393983/e76125b8-84ad-4639-81f3-ee7ba8cd89d7)

![sql7](https://github.com/vasundrasriravi/Ex-No-5-Creating-Triggers-using-PL-SQL/assets/119393983/f38a1ffe-9a2c-47ca-aa08-915a0b5c2de4)

### Result:
Thus the program for creating triggers has been implemented successfully.
