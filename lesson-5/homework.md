1. What are the three main methods to bulk insert data into SQL Server using SSIS?

2. In the File System Task, how do you configure SSIS to use a dynamic file path stored in a variable as the source?

3. What SSIS component allows you to organize multiple tasks into a single logical group?

4. In SSIS, what happens when you create two variables with the same name in different scopes?

5. Describe how the BatchSize and LastRow options influence the behavior of the SSIS Bulk Insert Task.

6. Provide an example of how to use a Script Task in SSIS to read a flat file line by line.

7. How do you remove the last comma from a list of values generated in a C# script in SSIS?

8. Explain how you would configure a File System Task to delete a specific file after it has been processed.

9. What are the benefits of using a Sequence Container in large SSIS packages?




Task 1: Bulk Insert Using Flat File Source
Goal: Import data from a flat file (vendors.txt) into SQL Server table Vendors.
(you can use your own path)
Steps:
Use a flat file (vendors.txt - ID,Name,Category)
Create a SQL table:
CREATE TABLE Vendors (
    ID INT,
    Name NVARCHAR(100),
    Category NVARCHAR(100)
);

In SSIS:
Use a Flat File Source to read the file.
Use Data Conversion if necessary.
Use an OLEDB Destination to insert data into Vendors.


After importing data, move the flat file vendors.txt from C:\SSIS\Source to C:\SSIS\Archive.
(you can use your own paths)
Steps:
Create a variable User::SourceFile with value C:\SSIS\Source\vendors.txt.
Use File System Task to move the file


Task 2: Use Script Task to Generate INSERT Statements
Goal: Read a file (products.txt - ID,Name,Price) and dynamically insert records into Products table using a Script Task.

CREATE TABLE Products (
    ID INT,
    Name NVARCHAR(100),
    Price INT
);


Steps:
Use Script Task to read the file.
Remove the header row.
Generate SQL INSERT statements with single quotes and no trailing commas.
Use connection string inside the script to execute each insert.

