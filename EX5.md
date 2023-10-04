# Ex. No: 5 Creating Triggers using PL/SQL

### AIM: To create a Trigger using PL/SQL.

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
 CREATE TABLE employee7( empid NUMBER,empname VARCHAR(10),dept VARCHAR(10), salary NUMBER);
 CREATE TABLE sal_log1 (log_id NUMBER GENERATED ALWAYS AS IDENTITY,empid NUMBER,empname 
 VARCHAR2(10),old_salary NUMBER,new_salary NUMBER,update_date DATE);

-- Insert the values in the employee table
 insert into employee7 values(1,'ren','marketing',50000);
 insert into employee7 values(2,'thyme','finance',55000);
 insert into employee7 values(3,'bright','HR',30000);
```

### Create employee table
```
CREATE TABLE employee7( empid NUMBER,empname VARCHAR(10),dept VARCHAR(10), salary NUMBER);
```

### Create salary_log table
```
CREATE TABLE sal_log1 (log_id NUMBER GENERATED ALWAYS AS IDENTITY,empid NUMBER,empname VARCHAR2(10),old_salary NUMBER,new_salary NUMBER,update_date DATE);
```


### PLSQL Trigger code
```
-- Create the trigger
CREATE OR REPLACE TRIGGER log_salary1_update
  2  BEFORE UPDATE ON employee7
  3  FOR EACH ROW
  4  DECLARE
  5    old_salary NUMBER;
  6    new_salary NUMBER;
  7  BEGIN
  8    old_salary := :OLD.salary;
  9    new_salary := :NEW.salary;
 10    IF old_salary <> new_salary THEN
 11      INSERT INTO sal_log1(empid, empname, old_salary, new_salary, update_date)
 12      VALUES(:OLD.empid, :OLD.empname, old_salary, new_salary, SYSDATE);
 13    END IF;
 14  END;
 15  /

-- Insert the values in the employee table
 insert into employee7 values(1,'ren','marketing',50000);
 insert into employee7 values(2,'thyme','finance',55000);
 insert into employee7 values(3,'bright','HR',30000);

-- Update the salary of an employee
 update employee7
  2  set salary= 89000
  3  where empid=2;

-- Display the employee table
SELECT * FROM employee7;

-- Display the salary_logg table
SELECT * FROM sal_log1;
```

### Output:
![dbms 5 op1](https://github.com/AtchayaSundaramoorthy/Ex-No-5-Creating-Triggers-using-PL-SQL/assets/119393516/0ee0b0ca-1119-4781-8bb5-7413a712063f)

![dbms 5 op2](https://github.com/AtchayaSundaramoorthy/Ex-No-5-Creating-Triggers-using-PL-SQL/assets/119393516/27c8860d-fce5-40ee-8a71-0c434537718a)

### Result:
Thus , the output has been successfully verified.
