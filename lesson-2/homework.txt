1. What are the key differences between a Data Flow Task and an Execute SQL Task?
Give one scenario for each. 

2. Why is a Data Conversion component often required when bringing data from a flat file into a Data Flow? What common problem does it solve?

3. List the three key properties you must configure inside an Execute SQL Task.

4. Which .NET namespaces are commonly imported when working with files and database connections in a Script Task?

5. Describe the purpose of a package-level variable.

6. Explain how a UNION ALL transformation works in SSIS.
What requirement must each input share before you can union them?

7. What error appears if the Excel source and Flat File source have mismatched data types at union time, and how can fix it?

8. SSIS variables can be used inside a Script Task.
How do you read the value of an SSIS variable in C#?

9. Truncating destination table before inserting often used.
a. Why is truncation important?
b. How would results differ if you omitted the truncate?

 Practical Tasks:

Task 1: Combine and Compare Two Data Sources
You have two customer lists—one from Excel, one from a pipe‑delimited TXT file. Both contain name, email, and signup date, but schemas differ slightly (column order, data types).

Deliverable: An SSIS Data Flow that ingests both sources, converts all fields to a common set of data types, and merges them with Union All.

Data Sources:

Customers.xlsx

Orders.txt
Key details:
Pipe delimiter instead of comma → Flat File Connection must match delimiter.
Blank or dash in Comments → must treat “–” as empty or NULL.
Quoted text around Comments

SQL Tables:
IF OBJECT_ID('dbo.Customers', 'U') IS NOT NULL DROP TABLE dbo.Customers;
GO
CREATE TABLE dbo.Customers (
    CustomerID   INT           PRIMARY KEY,
    FirstName    VARCHAR(50)  NOT NULL,
    LastName     VARCHAR(50)  NOT NULL,
    Email        VARCHAR(100) NOT NULL,
    SignupDate   DATE         NOT NULL,
    Notes        VARCHAR(200) NULL
);
GO

IF OBJECT_ID('dbo.Orders', 'U') IS NOT NULL DROP TABLE dbo.Orders;
GO
CREATE TABLE dbo.Orders (
    OrderID      INT           PRIMARY KEY,
    CustomerID   INT           NOT NULL,
    OrderDate    DATE          NOT NULL,
    TotalAmount  DECIMAL(10,2) NOT NULL,
    Comments     VARCHAR(200) NULL
);
GO



Task 2: Generate a new text file by exporting a SQL Server table of Grand Prix venues into it

Background:
You already ran the provided SQL script in Management Studio to create a table named GrandPrixRaces, which holds the full 2023 Formula One schedule. Your task is to build an SSIS package that reads every row from that table and writes it out to a plain‑text file.


Flat‑File Connection: a connection configured to write a new text file (for example, List of Grand Prix races for 2023.txt). Be sure to set the correct delimiter and text‑qualifier options, and indicate whether the file includes a header row.

Data Flow
Use GrandPrixRaces as the source.
Send the output directly into your Flat File Destination.

Output File
When you run the package, it must produce a text file containing all columns and rows from GrandPrixRaces.


SQL table :
CREATE TABLE GrandPrixRaces(
	GrandPrixId int IDENTITY(1,1) NOT NULL PRIMARY KEY,
	RoundNumber int NOT NULL,
	GrandPrix [varchar](255) NOT NULL,
	Circuit [varchar](255) NOT NULL,
	RaceDate [datetime] NOT NULL
) 
GO

INSERT GrandPrixRaces (RoundNumber, GrandPrix, Circuit, RaceDate) VALUES (1, N'Bahrain Grand Prix', N' Bahrain International Circuit, Sakhir', CAST(N'2023-03-05T00:00:00.000' AS DateTime))
GO
INSERT GrandPrixRaces (RoundNumber, GrandPrix, Circuit, RaceDate) VALUES (2, N'Saudi Arabian Grand Prix', N' Jeddah Corniche Circuit, Jeddah', CAST(N'2023-03-19T00:00:00.000' AS DateTime))
GO
INSERT GrandPrixRaces (RoundNumber, GrandPrix, Circuit, RaceDate) VALUES (3, N'Australian Grand Prix', N' Albert Park Circuit, Port Phillip', CAST(N'2023-04-02T00:00:00.000' AS DateTime))
GO
INSERT GrandPrixRaces (RoundNumber, GrandPrix, Circuit, RaceDate) VALUES (4, N'Azerbaijan Grand Prix', N' Baku City Circuit, Baku', CAST(N'2023-04-30T00:00:00.000' AS DateTime))
GO
INSERT GrandPrixRaces (RoundNumber, GrandPrix, Circuit, RaceDate) VALUES (5, N'Miami Grand Prix', N' Miami International Autodrome, Miami Gardens, Florida', CAST(N'2023-05-07T00:00:00.000' AS DateTime))
GO
INSERT GrandPrixRaces (RoundNumber, GrandPrix, Circuit, RaceDate) VALUES (6, N'Monaco Grand Prix', N' Circuit de Monaco, Monaco', CAST(N'2023-05-28T00:00:00.000' AS DateTime))
GO
INSERT GrandPrixRaces (RoundNumber, GrandPrix, Circuit, RaceDate) VALUES (7, N'Spanish Grand Prix', N' Circuit de Barcelona-Catalunya, Montmeló', CAST(N'2023-06-04T00:00:00.000' AS DateTime))
GO
INSERT GrandPrixRaces (RoundNumber, GrandPrix, Circuit, RaceDate) VALUES (8, N'Canadian Grand Prix', N' Circuit Gilles Villeneuve, Montreal', CAST(N'2023-06-18T00:00:00.000' AS DateTime))
GO
INSERT GrandPrixRaces (RoundNumber, GrandPrix, Circuit, RaceDate) VALUES (9, N'Austrian Grand Prix', N' Red Bull Ring, Spielberg', CAST(N'2023-07-02T00:00:00.000' AS DateTime))
GO
INSERT GrandPrixRaces (RoundNumber, GrandPrix, Circuit, RaceDate) VALUES (10, N'British Grand Prix', N' Silverstone Circuit, Silverstone', CAST(N'2023-07-09T00:00:00.000' AS DateTime))
GO
INSERT GrandPrixRaces (RoundNumber, GrandPrix, Circuit, RaceDate) VALUES (11, N'Hungarian Grand Prix', N' Hungaroring, Mogyoród', CAST(N'2023-07-23T00:00:00.000' AS DateTime))
GO
INSERT GrandPrixRaces (RoundNumber, GrandPrix, Circuit, RaceDate) VALUES (12, N'Belgian Grand Prix', N' Circuit de Spa-Francorchamps, Stavelot', CAST(N'2023-07-30T00:00:00.000' AS DateTime))
GO
INSERT GrandPrixRaces (RoundNumber, GrandPrix, Circuit, RaceDate) VALUES (13, N'Dutch Grand Prix', N' Circuit Zandvoort, Zandvoort', CAST(N'2023-08-27T00:00:00.000' AS DateTime))
GO
INSERT GrandPrixRaces (RoundNumber, GrandPrix, Circuit, RaceDate) VALUES (14, N'Italian Grand Prix', N' Monza Circuit, Monza', CAST(N'2023-09-03T00:00:00.000' AS DateTime))
GO
INSERT GrandPrixRaces (RoundNumber, GrandPrix, Circuit, RaceDate) VALUES (15, N'Singapore Grand Prix', N' Marina Bay Street Circuit, Singapore', CAST(N'2023-09-17T00:00:00.000' AS DateTime))
GO
INSERT GrandPrixRaces (RoundNumber, GrandPrix, Circuit, RaceDate) VALUES (16, N'Japanese Grand Prix', N' Suzuka International Racing Course, Suzuka', CAST(N'2023-09-24T00:00:00.000' AS DateTime))
GO
INSERT GrandPrixRaces (RoundNumber, GrandPrix, Circuit, RaceDate) VALUES (17, N'Qatar Grand Prix', N' Lusail International Circuit, Lusail', CAST(N'2023-10-08T00:00:00.000' AS DateTime))
GO
INSERT GrandPrixRaces (RoundNumber, GrandPrix, Circuit, RaceDate) VALUES (18, N'United States Grand Prix', N' Circuit of the Americas, Austin, Texas', CAST(N'2023-10-22T00:00:00.000' AS DateTime))
GO
INSERT GrandPrixRaces (RoundNumber, GrandPrix, Circuit, RaceDate) VALUES (19, N'Mexico City Grand Prix', N' Autódromo Hermanos Rodríguez, Mexico City', CAST(N'2023-10-29T00:00:00.000' AS DateTime))
GO
INSERT GrandPrixRaces (RoundNumber, GrandPrix, Circuit, RaceDate) VALUES (20, N'São Paulo Grand Prix', N' Interlagos Circuit, São Paulo', CAST(N'2023-11-05T00:00:00.000' AS DateTime))
GO
INSERT GrandPrixRaces (RoundNumber, GrandPrix, Circuit, RaceDate) VALUES (21, N'Las Vegas Grand Prix', N' Las Vegas Strip Circuit, Paradise, Nevada[c]', CAST(N'2023-11-18T00:00:00.000' AS DateTime))
GO
INSERT GrandPrixRaces (RoundNumber, GrandPrix, Circuit, RaceDate) VALUES (22, N'Abu Dhabi Grand Prix', N' Yas Marina Circuit, Abu Dhabi', CAST(N'2023-11-26T00:00:00.000' AS DateTime))
GO


