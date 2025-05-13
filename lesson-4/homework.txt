1. In an SSIS Package Execute SQL Task that returns one value from a SQL query what ResultSet type must be selected?

2. What is the purpose of Parameter Mapping in Execute SQL Task and how does the indexing of question marks (?) relate to it?

3. Describe how you can view the value stored in an SSIS variable at runtime using Breakpoints.

4. Explain how to configure a Script Task to print a string variable named @StudentName. Provide the C# line used for display.

5. How do you use two separate SQL queries in SSIS where the first query stores its result in a variable, and the second one uses that variable as a parameter?

6. In an Execute SQL Task with multiple parameters (?), how do you match variables to specific positions?

7. What is the role of DelayValidation when working with dynamic file paths?

8. What happens if a result set is set to "Full Result Set" but the SQL query only returns a single value?




Task 1: Median Finder and Reporter

Build a package that:
Uses an Execute SQL Task to run the query below on the table Scores.
Stores the median score in a variable called User::MedianScore.
Displays that value using a Script Task.
write SQL Median Query in Execute SQL Task

SQL Setup:

CREATE TABLE Scores (
    ID INT PRIMARY KEY,
    Score INT
);

INSERT INTO Scores (ID, Score) VALUES
(1, 65), (2, 70), (3, 75), (4, 80), (5, 85);




Task 2: Parameter Mapping with Student Info

Build a package that:
Has a table StudentInfo with Name and City.
Runs a SQL Task to retrieve Name and City from a Given Student_Id which is stored in a Variable.
Stores results in variables and prints them in Script Task.

SQL Setup:

CREATE TABLE StudentInfo (
    ID INT,
    Name VARCHAR(50),
    City VARCHAR(50)
);

INSERT INTO StudentInfo VALUES
(1, 'Shohrux', 'Tashkent'),
(2, 'Aziza', 'Samarkand'),
(3, 'Bekzod', 'Namangan');





Task 3: Auto-Named Flat File Exporter

Create a package that:
Has a Data Flow Task pulling from SQL table Employee.
Writes output to a flat file named Employees_<timestamp>.txt.
Uses a variable with GETDATE() converted to string as part of the file name.
Output goes to C:\SSIS\Outputs\. or (your own path)

SQL Setup:

CREATE TABLE Employee (
    ID INT,
    Name NVARCHAR(50),
    Salary INT
);

INSERT INTO Employee VALUES
(1, 'Ali', 1000),
(2, 'Zarina', 1200),
(3, 'Murod', 1100);

