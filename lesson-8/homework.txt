1. What SSIS container is used to repeat a set of tasks a fixed number of times or across a date range?

2. How is the EvalExpression used in a For Loop Container?

3. In SSIS C#, what method is used to trim trailing commas from a string?

4. What C# method is used to create a new text file if it doesn’t exist?

5. How do you concatenate date and text in SSIS to form a file name like test_2024_05_12.txt?

6. What property or technique allows dynamic file creation in a loop without failing validation early?

7. How would you dynamically append each even number in a loop to a CSV file without overwriting previous entries each iteration?




Task 1: Insert Even Numbers into SQL Table via Script Task
Goal: Use a For Loop Container to loop numbers 1–50. Inside the loop, use a Script Task to dynamically build and insert even numbers into a SQL table named EvenNumbers.

SQL Table Setup:

CREATE TABLE EvenNumbers (
    Value INT
);



Task 2: 

Build an SSIS package that loops through all days of the current month and creates a .txt file for each day. Based on whether the day is a weekday or weekend, save the file into a different folder:

Weekday files → C:\Logs\Weekdays\
Weekend files (Saturday & Sunday) → C:\Logs\Weekends\
(You can use your own path)

File Output Requirements:
Each file should be named in the format:
log_YYYY_MM_DD.txt
File content should simply include a line like:
"Log for 2024-05-12 - Sunday"
File paths must be dynamically generated based on the looped date.

Key SSIS Components Required:
For Loop Container to iterate from the 1st to the last day of the current month.
Expression Task or Script Task to determine the weekday number (1 = Sunday to 7 = Saturday).
Precedence Constraints to direct file creation to the correct folder path.
Two Script Tasks (or one reusable) to generate the .txt file in the proper destination.

Variables for:
StartDate (date, starts on 1st)
EndDate (1st of next month)
CurrentDate (loop variable)
WeekdayNumber (1–7)
FormattedFileName (e.g., log_2024_05_12.txt)
FullPath (concatenated folder path + filename)
WeekdayFolder, WeekendFolder
(Or you can do with your logic variables)
