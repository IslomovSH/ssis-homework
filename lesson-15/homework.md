Lesson 15: OLTP / OLAP, SCD Type 0, CDC

1. Explain the main differences between OLTP and OLAP systems. Provide an example use case for each.
2. What does SCD stand for in data warehousing? Describe SCD Type 0.
3. What is the purpose of the AK suffixed columns field in a DW table?
4. Describe how a Lookup transformation helps prevent duplicate data during an ETL process.
5. Why is it important to track the last successful load date in an ETL process?
6. What are the types of operations logged in a CDC system table?
7. Why might we avoid mapping all columns in a Lookup transformation during ETL?
8. What is Change Data Capture (CDC) and why is it useful in incremental ETL processes?
9. Explain the difference between Insert (2), Update (4), and Delete (1) operations in CDC.
10. What are some advantages of using an OLAP database for reporting over an OLTP system?
11. In a real-world ETL process, what could go wrong if the loaddate is not properly maintained or updated?

✅ Task 1 – Implement SCD Type 0 for a Product Table
Goal: Migrate product data from OLTP to OLAP using SCD Type 0 strategy with derived columns and Lookup.

Source: OLTP.dbo.Product
Destination: OLAP.dbo.DimProduct

Steps:

Create source and destination tables:

-- OLTP
CREATE TABLE Product (
  ProductID INT PRIMARY KEY,
  ProductName VARCHAR(50),
  Category VARCHAR(30),
  ModifiedDate DATETIME
);

-- OLAP
CREATE TABLE DimProduct (
  ProductSK INT IDENTITY(1,1) PRIMARY KEY,
  ProductAK INT,
  ProductName VARCHAR(50),
  Category VARCHAR(30),
  LoadDate DATETIME
);

Build SSIS package with:

OLE DB Source: Select ProductID, ProductName, Category from OLTP.

Derived Column: Add LoadDate = GETDATE().

Lookup: Match on ProductAK to avoid duplicates.

OLE DB Destination: Insert only new products into DimProduct.

✅ Task 2 – Build Incremental Load with LastModifiedDate Check
Goal: Perform incremental load using ModifiedDate and LastSuccessfulLoadDate comparison logic.

Source: OLTP.dbo.Employee
Destination: OLAP.dbo.DimEmployee
Audit Table: OLAP.dbo.ETL_EmployeeAudit

Steps:

Create tables:
CREATE TABLE Employee (
  ID INT PRIMARY KEY,
  FullName VARCHAR(50),
  Department VARCHAR(30),
  ModifiedDate DATETIME
);

CREATE TABLE DimEmployee (
  EmployeeSK INT IDENTITY(1,1),
  EmployeeAK INT,
  FullName VARCHAR(50),
  Department VARCHAR(30),
  LoadDate DATETIME
);

CREATE TABLE ETL_EmployeeAudit (
  ID INT IDENTITY(1,1),
  LastSuccessfulLoadDate DATETIME
);

SSIS Package:

Use Execute SQL Task to get latest audit date into @LastLoadDate.

Use OLE DB Source to filter: WHERE ModifiedDate > ?

Use Derived Column to add LoadDate.

Use Lookup on EmployeeAK to avoid duplicates.

At end, use Execute SQL Task to insert GETDATE() into ETL_EmployeeAudit.











