Lesson 18 :Access Control

1.How do you create a SQL Server login and user?
2.What permissions are required for a user to see data from tables?
3.How do you grant INSERT, UPDATE, and DELETE permissions on a table?
4.What SQL statement is used to check existing permissions on a specific table?
5.What happens when a user without proper permissions tries to update a table?
6.What is the SQLAgentOperatorRole and what permissions does it provide?
7.What’s the difference between SQLAgentUserRole, SQLAgentReaderRole, and SQLAgentOperatorRole?
8.Why is permission management important in a multi-user SQL Server environment?
9.What is the purpose of the GRANT command in SQL Server?
10.Why should access to SSIS packages and jobs be restricted to certain roles?
11.What is the difference between Login and User in SQL Server?



Task 1: Grant and Test Table Permissions
Create a user named report_user in the OLAP database. Grant this user only SELECT and INSERT permissions on the table dbo.factSales. Then test that the user can insert data but cannot update existing records. Provide screenshots of your attempt.



Task 2: Verify Permissions on a Table
Using the sys.database_permissions and sys.database_principals views, write a SQL query to display all permissions assigned on the table dbo.factSales. Execute the query and explain what permissions the user report_user has.



Task 3: SQL Server Agent Role Assignment
Create a login job_manager, map it to a user in the msdb database, and assign it to the SQLAgentReaderRole. Then, verify and explain what job-related permissions this role provides by attempting to view and execute existing SQL jobs.



Task 4: Escalate Permissions and Audit
Update the permissions for the user report_user by granting UPDATE and DELETE rights on the table dbo.factSales. Then rerun your earlier query to confirm the permissions have been changed. Explain each result.


Task 5: Create and Secure a New Table
As a system admin, create a new table named dbo.EmployeeAudit in the OLAP database with columns (EmpID INT, ActionType VARCHAR(20), ActionDate DATETIME). Grant INSERT permission only to the user auditor_user. Try running UPDATE and DELETE from that user and show that they're denied.








