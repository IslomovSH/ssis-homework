1. What SSIS container allows you to loop through all files in a directory?

2. In a Foreach Loop Container, what enumerator type should be selected to loop through file names?

3. How do you make the Flat File Connection dynamic inside a Foreach Loop?

4. What is the purpose of setting DelayValidation = True in a Data Flow Task?

5. In C#, how do you exclude the header row (first line) from a file being processed?

6. How can you filter only .txt files using Foreach Loop?

7. Describe how to insert data into SQL Server using a Script Task with dynamically generated INSERT statements.

8. How can you display the full file path for each file inside a Script Task?

9. What changes are needed in a Flat File Connection Manager to allow importing a different file every loop?



Task 1: Looping Over Files – Importing Big Bang Theory Data
Objective:
Create an SSIS package that loops through multiple .csv files using a Foreach Loop Container and loads their content into the SQL table BigBangEpisodes.

Files and Tables
Source Folder:
Big bang theory season 7.csv
Big bang theory season 8.csv
Big bang theory season 9.csv
Big bang theory season 10.csv


CREATE TABLE BigBangEpisodes (
    SeasonNumber INT NULL,
    EpisodeNumber INT NULL,
    DateBroadcast DATE NULL,
    Title VARCHAR(255) NULL
);


Task Instructions:
Create a folder on your PC: C:\SSIS\BigBangData (you can use your path)
Place multiple .csv files there (e.g., Season 7, 8, 9 10 files).
Each file should follow the same structure (same as the uploaded file).

Create a package which loops over the CSV files (give files ...Season 7, 8, 9 10 files)) in the folder path, importing each into the table BigBangEpisodes to get the data 

You'll need at some stage to create an expression for the ConnectionString property of the flat file connection.  Note: you're not allowed to use the MultiFlatFile connection - that would be cheating!



