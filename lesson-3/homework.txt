1. What is the purpose of the Multicast transformation in SSIS? Provide a use-case where it is necessary.

2. What is the difference between Delimited and Fixed Width text formats in Flat File sources?

3. How can you change the code page in a flat file connection?

4. Describe the process of using the Derived Column transformation to add a LoadDate column with the current date.

5. How can you create a conditional column such as “Senior” or “Junior” based on an age column in Derived Column?

6. What happens if column names in the first row of a flat file are not checked? How does it affect column mapping?

7. Explain how to use a Script Task and Variable to count rows in SSIS and print them using C#.

8. How do you enable and use a Data Viewer in the data flow to debug your transformation?

9. What is the role of a breakpoint in SSIS, and how is it used to monitor variables?

Task 1: Build and Test a Union All with Three Sources
Goal: Combine data from an Excel file (Students.xlsx), Flat File (students.txt), and a SQL table (AllStudents).

Steps:
Create a new SSIS project.
Add a Data Flow Task.
Add three sources: Excel Source, Flat File Source, OLE DB Source (SQL).
Match all mismatched data types with destination.
Use Union All to merge all three data streams.
Add a Derived Column to insert GETDATE() as LoadDate.
Output the final result to the AllStudents table using OLE DB Destination.

Task 2: Add Derived and Conditional Columns
Goal: Enrich the student data with calculated columns.
Steps:

After combining sources using Union All, insert a Derived Column.
Add:

LoadDate with GETDATE().
AgeCategory column: IF Age < 25 then 'Junior', Age between 25 and 30 THEN 'Middle' ELSE 'Senior'.
Connect the output to AllStudents SQL table and run the package.


Task 3: Debug Row Count with Script Task
Goal: Monitor how many rows are processed.

Steps:
Add a variable named RowCounter (int).
Insert a Row Count transformation after any source and connect it to RowCounter.
In a script, write C# code to print the row count


Table script:
CREATE TABLE AllStudents (
    ID INT,
    Name NVARCHAR(50),
    Age INT,
    Email NVARCHAR(100),
    AgeCategory NVARCHAR(20),
    LoadDate DATETIME
);



Optional Extra Table (if needed for testing union):



CREATE TABLE SQLStudents (
    ID INT,
    Name NVARCHAR(50),
    Age INT,
    Email NVARCHAR(100)
);

INSERT INTO SQLStudents (ID, Name, Age, Email) VALUES
(11, 'Rustam', 31, 'rustam@example.com'),
(12, 'Zarina', 22, 'zarina@example.com'),
(13, 'Timur', 27, 'timur@example.com');



