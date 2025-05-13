1. Define an SSIS Project and an SSIS Package.
How are they related, and why might one project contain multiple packages?

2. What is a “Source” in SSIS?
List three common source types and give a brief example of when you’d use each.

3. What is a “Destination” in SSIS?
List three common destination types and describe a scenario for each.

4. Describe the difference between Control Flow and Data Flow.

5. What prerequisite must you install to use Excel Source/Destination components? 




Task: Simple Data Flow – Flat File → SQL Server

Create a package to ingest external CSV data into SQL Server

Requirements:
A Flat File Connection Manager pointing at your CSV.
An OLE DB Connection Manager pointing at your SQL Server database.

A Data Flow containing:
Flat File Source
OLE DB Destination

Instructions:

YOU HAVE A CSV FILE THAT CONTAINS(EMPLOYEES) DATA.
(EmployeeID,FirstName,LastName,Department,HireDate,Salary)
YOUR TASK IS TO LOAD THIS DATA INTO AN SQL TABLE CALLED EMPLOYEES:
IF OBJECT_ID('dbo.Employees', 'U') IS NOT NULL
    DROP TABLE dbo.Employees;
GO

CREATE TABLE dbo.Employees (
    EmployeeID   INT         NOT NULL
  , FirstName    NVARCHAR(50) NOT NULL
  , LastName     NVARCHAR(50) NOT NULL
  , Department   NVARCHAR(50) NOT NULL
  , HireDate     DATE        NOT NULL
  , Salary       INT         NOT NULL
);
GO

USE DATA FLOW TASK
INSIDE OF IT USE FLATFILE SOURCE AND OLE DB DESTINATION TO TRANSFORM THE DATA
