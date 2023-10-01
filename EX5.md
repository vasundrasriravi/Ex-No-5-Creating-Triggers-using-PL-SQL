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
```
CREATE TABLE employe(
  empid NUMBER,
  empname VARCHAR2(10),
  dept VARCHAR2(10),
  salary NUMBER
);

CREATE TABLE salary_log (
  log_id NUMBER GENERATED ALWAYS AS IDENTITY,
  empid NUMBER,
  empname VARCHAR2(10),
  old_salary NUMBER,
  new_salary NUMBER,
  update_date DATE
);
-- Insert the values in the employee table
insert into employe values(1,'Kar','IT',1000000);
insert into employe values(2,'Boha','SALES',500000)
```
### Create employee table
![employee](https://github.com/vasundrasriravi/Ex-No-5-Creating-Triggers-using-PL-SQL/assets/119393983/2a29b107-21e0-4fd1-91f3-65c1639cc265)

### Create salary_log table
![salary](https://github.com/vasundrasriravi/Ex-No-5-Creating-Triggers-using-PL-SQL/assets/119393983/871a83fa-367e-483f-a227-2df91b774bf0)

### PLSQL Trigger code
```
-- Create the trigger
CREATE OR REPLACE TRIGGER log_sal_update
BEFORE UPDATE ON employe
FOR EACH ROW
BEGIN
  IF :OLD.salary != :NEW.salary THEN
    INSERT INTO sal_log (empid, empname, old_salary, new_salary, update_date)
    VALUES (:OLD.empid, :OLD.empname, :OLD.salary, :NEW.salary, SYSDATE);
  END IF;
END;
/
-- Insert the values in the employee table
insert into employe values(1,'Kar','IT',1000000);
insert into employe values(2,'Boha','SALES',500000);

-- Update the salary of an employee
UPDATE employe
SET salary = 60000
WHERE empid = 1;
-- Display the employee table
SELECT * FROM employe;

-- Display the salary_log table
SELECT * FROM sal_log;
```
### Output:
![log](https://github.com/vasundrasriravi/Ex-No-5-Creating-Triggers-using-PL-SQL/assets/119393983/908c6ddc-0e11-4fd0-b7df-5c42702a97e2)

### Result:
Thus the program for creating triggers has been implemented successfully.
