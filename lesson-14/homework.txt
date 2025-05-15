Lesson 14: Project Deployment, Configuration, SQL Jobs

1. What are the key differences between package deployment and project deployment in SSIS?
2. Why is it important to use configurations in SSIS, especially when working with different environments like development and production?
3. List and explain the types of configuration options available in SSIS.
4. Describe the steps to configure a package to use an XML configuration file.
5. How can you override a package parameter (like empID) using the SQL Server configuration?
6. Explain how to deploy an SSIS project using SQL Server Data Tools and how to link configuration values.
7. What is a SQL Job and give three real-world examples where it can be useful.
8. How do you create and use variables in an SSIS package?
9. What is the significance of using Result Set in SSIS and how is it different from Execute SQL without a result set?
10. Why is it important to separate development and production environments?


🎯 Task 1: Multi-Environment Dynamic Package Execution with Configuration Switch
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

🎯 Task 2: Complex Project Deployment with Parameterized Job Scheduling
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

🎯 Task 3: Error-Handled Job Execution and Dynamic Configuration Validation
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