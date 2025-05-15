1. What Foreach enumerator type is used in SSIS to loop through Excel worksheet names?

2. What is the difference between Table Catalog, Table Schema, Table Name, and Table Type in the ADO schema rowset?

3. Describe how to loop through all Excel files in a folder using the Foreach Loop.

4. How do you make the Excel Connection Manager dynamically change its path using an SSIS variable?

5. How can you print the iteration value of a For Loop using a Script Task?

6. How do you use parameter mapping in an Execute SQL Task to insert variable values into a SQL table?

7. How do you dynamically assign an Excel sheet name to a variable during a loop?

8. How can you insert only even numbers from 5 to 50 into a SQL table using a For Loop in SSIS?




Task 1: Use a dynamic connection to loop over Excel workbooks, combining their rows into a SQL Server table

You're given three Excel files (Anyone.xlsx, Elderly.xlsx, and Toddlers.xlsx), each containing a music playlist for a different target group. All files have the same structure with columns: Artist, Song, and TargetMarket. Your job is to build an SSIS package that loops through these files and inserts all records into a single SQL Server table named PlayList.

Use a Foreach Loop Container to iterate through the Excel files stored in a folder. Inside the loop, dynamically update the Excel connection string to read from the current file. Load the data from each file's Sheet1 into the SQL table.

You must ensure the solution is dynamic and reusable:
Use SSIS variables for the file path.
Configure the connection manager to respond to file changes.
Set delay validation to allow dynamic behavior.

Excel Files:
Anyone.xlsx
Elderly.xlsx
Toddlers.xlsx

All contain the same columns:
Artist, Song, TargetMarket


CREATE TABLE PlayList (
    Artist NVARCHAR(255),
    Song NVARCHAR(255),
    TargetMarket NVARCHAR(255)
);



Task 2: 

You're given a set of Excel files (e.g., Trial A.xlsx, Trial B.xlsx, Trial D.xlsx) that each contain a list of ItemId and ItemName. A control table named BushtuckerImports specifies which trials (letters A, B, D, etc.) should be processed.

Your task is to build an SSIS package that loops through the rows in BushtuckerImports, dynamically constructs the path to each corresponding Excel file based on the ImportLetter value (e.g., "A" maps to Trial A.xlsx), and loads the data from each file into the BushtuckerData table.

Tables Involved
Control Table: BushtuckerImports (ImportLetter)
Target Table: BushtuckerData (ItemId, ItemName)

Source Files
Trial A.xlsx
Trial B.xlsx
Trial D.xlsx


CREATE TABLE BushtuckerData(
	ItemId int,
	ItemName nvarchar(255)
)

CREATE TABLE BushtuckerImports(
	ImportId int PRIMARY KEY IDENTITY(1,1),
	ImportLetter varchar(1)
)
GO

-- add letters
INSERT INTO BushtuckerImports(ImportLetter) VALUES('A')
INSERT INTO BushtuckerImports(ImportLetter) VALUES('B')
INSERT INTO BushtuckerImports(ImportLetter) VALUES('D')
GO

SELECT * FROM BushtuckerData
SELECT * FROM BushtuckerImports
