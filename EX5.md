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
CREATE TABLE employee12(
  empid NUMBER,
  empname VARCHAR2(10),
  dept VARCHAR2(10),
  salary NUMBER
);

CREATE TABLE logs_salary12 (
  empid NUMBER,
  empname VARCHAR2(10),
  old_salary NUMBER,
  new_salary NUMBER,
  update_date DATE
);
-- Insert the values in the employee table
insert into employee12 values(1,'Arya','HR',900000);
insert into employee12 values(2,'Nikita','Manager',700000);
insert into employee12 values(3,'Krishna','Finance',880000);
```

### Create employee table
```CREATE TABLE employee12(
  empid NUMBER,
  empname VARCHAR2(10),
  dept VARCHAR2(10),
  salary NUMBER
);
```

### Create salary_log table
```
CREATE TABLE logs_salary12 (
  log_id NUMBER,
  empid NUMBER,
  empname VARCHAR2(10),
  old_salary NUMBER,
  new_salary NUMBER,
  update_date DATE
);
```


### PLSQL Trigger code
```
-- Create the trigger
CREATE OR REPLACE TRIGGER logs_salary_update
BEFORE UPDATE ON employee12
FOR EACH ROW
BEGIN
  IF :OLD.salary != :NEW.salary THEN
    INSERT INTO sal_log (empid, empname, old_salary, new_salary, update_date)
    VALUES (:OLD.empid, :OLD.empname, :OLD.salary, :NEW.salary, SYSDATE);
  END IF;
END;
/
-- Insert the values in the employee table
insert into employee12 values(1,'Arya','HR',900000);
insert into employee12 values(2,'Nikita','Manager',700000);
insert into employee12 values(3,'Krishna',Finance',880000);
-- Update the salary of an employee
UPDATE employee12
SET salary = 990000
WHERE empid = 1;
-- Display the employee table
SELECT * FROM employee12;

-- Display the logs_salary12 table
SELECT * FROM logs_salary12;
```

### Output:
![image](https://github.com/aryabaisakhiya/Ex-No-5-Creating-Triggers-using-PL-SQL/assets/119393645/bebc2128-c009-432b-b701-36cc3cbbf461)



### Result:
Thus , the output has been successfully verified.
