Lesson 16: SCD 0, SCD 1 with Merge

1. What is SCD Type 0, and how is it implemented using a Merge Join in SSIS?
2. Why do we need to use Sort transformations before using Merge Join?
3. What does a Conditional Split do after a Merge Join in an SCD Type 0 flow?
4. How does SCD Type 1 differ from SCD Type 0 in terms of data updating?
5. What is the purpose of using a Derived Column in SCD workflows?
6. What is the role of a Lookup Transformation in identifying updated rows?
7. In SCD Type 1, what SQL operation helps in synchronizing the dim table with changes using query?
8. What is a Staging Table in SQL?
9. Why is it necessary to clear the staging table after loading data into the destination table?
10. Describe the use of OLE DB Command in updating records during ETL.
11. Why is logging important in SSIS ETL processes?


✅ Task 1 – SCD Type 0 using Merge Join for Customers
Goal: Use Merge Join to insert only new customers into the dimension table.

Source: OLTP.dbo.Customers
Destination: OLAP.dbo.DimCustomer

Steps:

Create tables:

-- OLTP
CREATE TABLE Customers (
  ID INT PRIMARY KEY,
  FullName VARCHAR(50),
  City VARCHAR(30),
  ModifiedDate DATETIME
);

-- OLAP
CREATE TABLE DimCustomer (
  CustomerSK INT IDENTITY(1,1),
  CustomerAK INT,
  FullName VARCHAR(50),
  City VARCHAR(30),
  LoadDate DATETIME
);

In SSIS:

Sort both OLTP and DimCustomer sources by ID.

Use Merge Join on ID = CustomerAK.

Use Conditional Split: ISNULL(CustomerAK) to identify new.

Add LoadDate = GETDATE() using Derived Column.

Insert into DimCustomer.




Task 2 – SCD Type 1 Direct Update for Product Table
Goal: Detect and update changes in product city using OLE DB Command.

Source: OLTP.dbo.Product
Destination: OLAP.dbo.DimProduct
Audit Table: OLAP.dbo.ETL_ProductAudit


Tables:
CREATE TABLE Product (
  ID INT PRIMARY KEY,
  Name VARCHAR(50),
  Category VARCHAR(50),
  ModifiedDate DATETIME
);

CREATE TABLE DimProduct (
  ProductSK INT IDENTITY(1,1),
  ProductAK INT,
  Name VARCHAR(50),
  Category VARCHAR(50),
  LoadDate DATETIME
);


SSIS Logic:

Fetch LastSuccessfulLoadDate from audit table.

In OLE DB Source: WHERE ModifiedDate > ?

Lookup on ProductAK

Conditional Split:

ISNULL(ProductAK) → insert

Category <> Category_Lookup → update via OLE DB Command

Insert current datetime as LoadDate

Update audit table at the end.




Task 3 – Use Staging Table and MERGE for Employee SCD 1
Goal: Insert/update employee records using staging table and MERGE.

Source: OLTP.dbo.Employees
Staging Table: OLAP.dbo.StagingEmployee
Destination: OLAP.dbo.DimEmployee
Audit Table: OLAP.dbo.ETL_EmployeeAudit



Tables:

CREATE TABLE Employees (
  ID INT PRIMARY KEY,
  Name VARCHAR(50),
  Department VARCHAR(30),
  ModifiedDate DATETIME
);

CREATE TABLE StagingEmployee (
  EmployeeAK INT,
  Name VARCHAR(50),
  Department VARCHAR(30),
  ModifiedDate DATETIME
);

CREATE TABLE DimEmployee (
  EmployeeSK INT IDENTITY(1,1),
  EmployeeAK INT,
  Name VARCHAR(50),
  Department VARCHAR(30),
  LoadDate DATETIME
);

SSIS:

Use Execute SQL Task to fetch LastSuccessfulLoadDate.

In Data Flow Task, load only changed/new rows into StagingEmployee.

Use Execute SQL Task to run MERGE to DimEmployee.

Truncate StagingEmployee afterward.

Update ETL_EmployeeAudit with current datetime.




