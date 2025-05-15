Lesson 10: Fuzzy LookUp, Parent and Child Package

1. On what Purpose we use Fuzzy LookUp in SSIS?
2. What does "Similarity Threshold" indicate?
3. Can we connect to other types of connections in Fuzzy LookUp?
If yes, what are they? If no, Why we can't?
4. What does Fuzzy LookUp return as output when it can't find any rows to compare with a specific data(column)?
5. Can we use Fuzzy LoopUp columns for Further transformations(can we get them to the destinations), what kind of downsides it could have?
6. What happens when we put "Similarity Threshold" to 1 in Fuzzy LookUp?
7. What are Parent and Child Packages and why do we use them?
8. Can we Pass values from the Parent package to a child Package ,if yes how?
9. Can we get values from the Child Package to the Parent Package,if yes how?



Tasks:

Task 1: Data Flow Basics with Fuzzy Lookup
Objective: Create a package that transforms data and uses Fuzzy Lookup to clean it.
Steps:

Use a Data Flow Task:

Read from a flat file(csv).

Apply Data Conversion to make the data types match with destination table and Derived Column transformations for logging load date.

Use a Fuzzy Lookup to match incoming customer names with a reference table and get customer_id.

Store the matched results in a destination table.(Orders)




Task 2: File Handling and Looping with Fuzzy Lookup
Objective: Loop through multiple files(products), process each with Fuzzy Lookup.
Steps:

Use a Foreach Loop Container to iterate over all CSV files in a folder.

Read data.

Apply Fuzzy Lookup to match entries against a master list (product names from ProductsReference table).

Save the cleaned data to your database.(Sales Table)

Wrap this logic into a Child Package. Use a Parent Package to loop through different directories that will get the directory from the parent package and use in it child package.



Task 3: Scheduling Logic and Fuzzy Lookup Integration
Objective: Automate scheduled data processing with fuzzy matching.

Use a For Loop Container that checks for a file(company_data.csv) every 30 minutes, up to 3 hours.

Use Script Task to check file presence and handle logic.

If file is found:

Process it with Fuzzy Lookup inside the Data Flow Task to Company Data table.





CREATE TABLE Orders (
    OrderID INT PRIMARY KEY,
    CustomerID INT,
    OrderAmount DECIMAL(10, 2),
    Inserted_at DATETIME,
    FOREIGN KEY (CustomerID) REFERENCES CustomersReference(CustomerID)
);

CREATE TABLE Sales (
    SaleID INT PRIMARY KEY,
    ProductID INT,
    Quantity INT,
    Price DECIMAL(10, 2),
    FOREIGN KEY (ProductID) REFERENCES ProductsReference(ProductID)
);

CREATE TABLE ProductsReference (
    ProductID INT PRIMARY KEY,
    ProductName VARCHAR(100)
);

INSERT INTO ProductsReference (ProductID, ProductName)
VALUES 
    (101, 'Smartphone X'),
    (102, 'Laptop Pro'),
    (103, 'Wireless Mouse'),
    (104, 'HDMI Cable'),
    (105, 'Portable Charger');



CREATE TABLE CompaniesReference (
    CompanyID INT PRIMARY KEY,
    CompanyName VARCHAR(100)
);

INSERT INTO CompaniesReference (CompanyID, CompanyName)
VALUES 
    (201, 'OpenAI Incorporated'),
    (202, 'Google LLC'),
    (203, 'Microsoft Corporation'),
    (204, 'Amazon'),
    (205, 'NVIDIA Corp');


CREATE TABLE CompanyData (
    CompanyID INT,
    CompanyName VARCHAR(100),
    Revenue DECIMAL(15, 2),
    FOREIGN KEY (CompanyID) REFERENCES CompaniesReference(CompanyID)
);





