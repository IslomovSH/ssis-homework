Lesson 17: SCD Type 2 with Merge and Lookup

1.What is SCD Type 2 and how does it maintain historical data?
2.What are the main differences between the OLAP and OLTP tables(students and dimstudents)?
3.What columns is usually used to identify changed data?
4.How is the MERGE statement structured for SCD Type 2 processing?
5.What role does "Enddate IS NULL" play in update logic for historical records?
6.How does the OLE DB Command update the current row during a lookup-based SCD Type 2 process?
7.Why is UNION ALL used after the OLE DB Command?
8.What is the significance of using parameters in an OLE DB Source query?
9.How can you truncate and refresh staging tables dynamically before load?
10.How is a full result set captured using variables in the Execute SQL Task?
11.Why is it better to avoid truncating the dimension table when tracking history?
12.What’s the difference between business key and alternate key in SCD?


Task 1: Multi-Environment Dynamic Package Execution with Configuration Switch
Objective:
Design and deploy an SSIS package that:

Contains Execute SQL Task fetching data from a table Employees in DEV database.

Use Project Deployment Model to SSISDB.

Implement three configurations:

XML File Configuration

SQL Server Table Configuration

SSISDB Environment Variable Configuration

Switch EmpID parameter dynamically between 1, 2, and 4 using these configurations.

Document how each configuration works and verify the output (EmpName) changes accordingly.

Requirements:

Use Script Task to log the selected EmpName into Execution_Audit table (ExecutionID, EmpID, EmpName, ConfigUsed).

Ensure configurations are interchangeable and validated by executing the package externally via SSISDB Catalog.




Task 2: Complex Project Deployment with Parameterized Job Scheduling
Objective:
Create an SSIS project with:

Two packages:

Package 1: Loads data from Orders_DEV to Orders_Archive_DEV.

Package 2: Archives error records to Error_Log_DEV.

Deploy the project to SSISDB/Production.

Set Project Parameters (LoadDate, ArchiveMode).

Create a SQL Server Agent Job that:

Executes Package 1 hourly.

Executes Package 2 nightly.

Uses Environment Variables for parameters.

Log the execution results into a custom table JobExecution_Audit (JobID, PackageName, ExecutionTime, Status).

Requirements:

Simulate an error in Package 1 and verify error handling and job step continuity.

Ensure Schedules are set to recurring (every 1 hour and daily at 11:59 PM).



Task 3: Error-Handled Job Execution and Dynamic Configuration Validation
Objective:
Create a complex SSIS package that:

Uses Execute SQL Task with a dynamic query using expressions.

Uses Package Parameters for Gender, MaritalStatus.

Integrate SSISDB Environment Variables with possible combinations (M-M, M-S, F-M, F-S).

Deploy the package to Production folder in SSISDB.

Create a SQL Agent Job that:

Executes the package using SSISDB Environment Variable mapping.

Validates the data extracted against expected counts in a verification table (Filter_Audit).

Logs errors into SSISDB logs and SQL table JobError_Audit (JobID, ErrorDetails, PackageName).

Requirements:

Simulate an error by providing an invalid combination.

Use Job History and custom logs to analyze the failure.

Disable the job after two consecutive failures.





