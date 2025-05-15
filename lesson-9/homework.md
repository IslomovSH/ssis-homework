


Task 1: Date Formatter with SQL, Expression, and C#
Goal: Format the current date to YYYY_MM_DD and use it in a file name variable.

Requirements:
Use three methods to set User::FormattedDate:
Execute SQL Task with CONVERT or FORMAT
Expression Task using REPLACE and LEFT
Script Task using C#
Output: Final file name should be log_YYYY_MM_DD.txt



Task 2: Design an SSIS package that continuously checks for the presence of a specific file (input.csv) in a folder (C:\SSIS\Input\). The package must:

Wait up to 2 hours for the file to arrive.
Check every 10 seconds.
Process the file immediately upon detection using a Data Flow Task.
Log either a success or timeout message (with timestamp) into a SQL table, depending on the outcome.
Stop execution gracefully whether the file appears or not.

CREATE TABLE FilePollingLog (
    LogTime DATETIME,
    StatusMessage NVARCHAR(255)
);

Key Requirements
Use a Script Task to implement a while loop in C#.

Inside the loop:
Compare current time to a predefined EndTime (e.g., GETDATE() + 2 hours).
If the file is found → Break loop → Run Data Flow Task → Log success.
If the file is not found → Sleep for 10 seconds → Continue loop.
If the time is exceeded → Log a timeout message → Exit loop cleanly.

Functional Expectations
The file should not be processed if the 2-hour window expires.
Log must clearly state:
"File received and processed successfully"
OR
"Timeout reached. File not received."
Use expressions to set EndTime dynamically when the package starts.

Folder and File Example
Folder: C:\SSIS\Input\
File to wait for: input.csv

(You can use your own path)

