Lesson 11 Error Handling. Introduction to precedence constraint.

1. Why do we need Error handling in SSIS?
2. What will happen if we will have "ignore failure" in the Error Output of a Source transformation(OLE DB, Excel, Flat File.....)
3. How do we get the time that error occurred in  a data flow task after applying "redirect rows" if failure appears?
4. How do we get the error column name and error description to a sql table?
5. What does Precedence Constraint do?
6. What does each color(Green, Blue, Red) of Precedence Constraint mean?
7.How many evaluation operations does a Precedence Constraint has?
8. What happens when we choose "Expression or Constraint" as Evaluation operation in precedence Constraint?
9. What is the Difference between "Logical AND" and "Logical OR" selections in the Precedence Constraint.
10. What transformation is used to send an email in SSIS?



Task 1:

Create a SSIS Package that has 3 Data Flow Tasks each loads data from different types of Files to an Orders table in SQL Server.
If any three of them fails while execution write the execution time, Data Flow Task name to a ErrorLog table in SQL Server using Execute SQL Task and load the rows that has problem with to a Orders_Error table


CREATE TABLE Error_Log (LogID INT IDENTITY(1,1), Package_Name VARCHAR(500), OccuredAt DATETIME);

CREATE TABLE Orders (
    OrderID INT PRIMARY KEY,
    CustomerName NVARCHAR(100),
    Product NVARCHAR(100),
    Quantity INT,
    Price DECIMAL(10, 2),
    OrderDate DATE
);

CREATE TABLE Orders_Error (
    OrderID VARCHAR(MAX),
    CustomerName VARCHAR(MAX),
    Product VARCHAR(MAX),
    Quantity VARCHAR(MAX),
    Price VARCHAR(MAX),
    OrderDate VARCHAR(MAX)
);


