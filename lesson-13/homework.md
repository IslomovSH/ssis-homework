Lesson 13: Lookup, Logging, Package Deployment

1.What is the purpose of the Lookup transformation in SSIS?
2.What columns are typically used to match source and reference data in a Lookup?
3.What are the different cache types available in Lookup, and when would you use “No Cache”?
4.How do you handle unmatched rows in a Lookup transformation?
5.Why do we create separate destinations for matched and unmatched data?
6.What is SSIS logging and what formats can it store log data in?
7.How do you enable logging for a package and choose the logging provider?
8.What events can be captured by SSIS logging (e.g., OnError, OnPreExecute)?
9.Describe the deployment process of an SSIS package to SSISDB.
10. What should be install to our SQL Server to be able to deploy a package(project)?
11.What is the use of the Execute SQL Task in SSIS?
12.How can variables be used inside expressions for SQL command customization?
13.What kind of enumerator type should be used in Foreach Loop container when looping through multiple rows from a variable?
14.What’s the difference between ResultSet = Single Row and ResultSet = Full Result Set?
15.How is the Script Task used to see  variable values?



🎯 Task 1: Multi-Lookup Data Quality Pipeline with Audit and Email Notification
Objective:
Design an SSIS package that:

Source: CSV file (Customer_Input.csv) containing FirstName, LastName.

Use Lookup Transformation against Customer_Master table (FirstName, LastName, City, Country).

Separate matched records to Customer_Valid table.

Send unmatched records to Customer_Invalid table.

Additionally: After processing:

Use Row Count Transformation to count unmatched records.

If unmatched records > 10, send an email alert to dataquality@company.com and log the count to the Audit_Quality table (ExecutionID, TotalRows, InvalidRows, Status).

Requirements:

Use Partial Cache in Lookup.

Use Data Viewer to visualize data flow.

Ensure all variables are properly defined.

🎯 Task 2: Custom Logging with SSIS and Verification via Script Task
Objective:
Create an SSIS package that:

Contains a Data Flow Task simulating ETL from Sales_Orders to Sales_Archive.

Configure Logging to both SQL Server (SSISLOG_Custom) and a text file (SalesLog.txt).

Ensure the package logs:

Task start/end.

Any warnings.

Any errors.

After execution, use a Script Task to:

Check the SSISLOG_Custom table.

Generate a report summary (Number of errors, Number of warnings).

Display the summary in the Script Task output window.

Requirements:

Use Sales_Orders table with at least 10 records.

Simulate an error by inserting invalid data deliberately into the flow.

🎯 Task 3: Dynamic Query Execution and Foreach Loop Display with Custom Formatting
Objective:
Build an SSIS package where:

Use Execute SQL Task connected to AdventureWorks database.

Use expressions to build dynamic query filtering:

Gender = 'F'

MaritalStatus = 'M'

Store the full result set into an Object variable ([User::FullResult]).

Use Foreach Loop Container with ADO Enumerator to:

Loop through all names.

Concatenate them into a formatted string using Expression Task (each name should be prefixed with line number, e.g., 1. Jane Doe).

At the end, display all names in a MessageBox using Script Task.

Requirements:

Use at least 20 records in the result set.

Create an additional variable ([User::FormattedNames]) to store the final string.