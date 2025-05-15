Lesson 12: Precedence Constraint (Continuation) and Transactions.


1. What is the difference between the arrows(lines that connects each transformation) in Data Flow and Control Flow?
2. Imagine you have 3 Data Flow Tasks and you have to run another Data Flow Task if all the other 3  completes Successfully(don't connect the first 3 to each other)
3. Is it possible to Control the Flow of the Execution based on Expressions in SSIS and how?
4.What is the DIfference Between "Expression and Constraint" and "Expression or Constraint" in the selection list of Precedence Constraint




🎯 Task 1: Advanced Control Flow with Dynamic Failure Handling and Email Notification
Objective:
Design an SSIS package where:

Execute SQL Task 1 simulates a data fetch (use WAITFOR DELAY '00:00:05').

If this task fails, the process must:

Trigger an email notification task using Send Mail Task.

Log the error details to a custom table (ExecutionLogs).

If the task succeeds, it must continue to Script Task 1.

Use Failure precedence constraint with expressions checking variable [User::isCritical] equals 1, ensuring the task is triggered only on both failure and condition.

Requirements:

Use the table ExecutionLogs (Columns: ExecutionID, TaskName, ErrorMessage).

The email should send to admin@example.com.

Use a user variable [User::isCritical] set initially to 1.

🎯 Task 2: Data Flow Row Validation and Exception Handling with Conditional Mail Trigger
Objective:
Create an SSIS package that:

Source: Table Employee_Source.

Destination: Table Employee_Destination.

Use Row Count Transformation to count the rows moved.

After data load, use Execute SQL Task to count rows in Employee_Destination.

Compare the row counts using Script Task and variables.

If row counts do not match, trigger Send Mail Task to qa_team@example.com.

If the task fails due to mismatch, log it into a table RowCountAudit (ExecutionID, SourceRows, DestRows, Status).

Requirements:

Email body should include the mismatch row counts.

Use exact table names.

Use appropriate expressions in constraints to handle flow accuracy.

🎯 Task 3: SQL Transaction Handling with SSIS Control Flow
Objective:
Simulate a money transfer process in SQL using Execute SQL Task in SSIS.

Create two accounts in table Accounts (AccountID, Balance).

Write a stored procedure sp_TransferAmount to:

Deduct from Sender.

Add to Receiver.

Use transactions (BEGIN TRAN, COMMIT, ROLLBACK) inside the procedure.

In SSIS, use Script Task to call the procedure twice:

First with valid ReceiverID.

Second with invalid ReceiverID.

If the second call fails, ensure ROLLBACK happens and log the error in TransactionAudit (TransferID, SenderID, ReceiverID, Amount, Status).

Requirements:

Simulate a failure by sending to a non-existing account.

The package should log the success/failure result explicitly to TransactionAudit.