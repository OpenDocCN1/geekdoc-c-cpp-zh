
## 5.1.2 Data Design Wizards in the Data Source Window ................ 180
### 5.1.2.1 Add New Data Source ............................................ 180
### 5.1.2.2 Data Source Configuration Wizard ........................ 181
### 5.1.2.3 DataSet Designer ................................................... 185
## 5.2 Build a Sample Database Project – SelectWith with SQL Server Database............... 187
### 5.2.1 Application User Interfaces ....................................... 187
### 5.2.1.1 The LogIn Form ................................................ 188
### 5.2.1.2 The Selection Form ................................... 192
### 5.2.1.3 The Faculty Form ........................................ 192
### 5.2.1.4 The Course Form ........................................ 193
### 5.2.1.5 The Student Form ....................................... 194
### 5.2.1.6 Using Five Words without Building Them ................ 195
## 5.3 Add and Utilize Visual.NET Wizards and Design Tools ................ 197
### 5.3.1 Add and Configure a New DataSet .......................... 197
## 5.4 Query and Display Data using the DataGridView View Control ................ 200
### 5.4.1 View the Entire Table ................................... 200
### 5.4.2 View Each Record or Selected Columns ................ 203
## 5.5 Use DataSet Designer to Edit the Structure of a DataSet ................ 204
## 5.6 Bind Data to the Associated Controls in LogIn Form ................ 207
## 5.7 Develop Controls to Query Data using the Filter() Method ................ 210
## 5.8 Return a Single Value to Query Data for LogIn Form ................ 212
## 5.9 Coding for the Selection Form ................................ 215
## 5.10 Bind Data to the Associated Controls in Faculty Form ................ 218
## 5.11 Develop Controls to Query Data using the SQL SELECT Method ................ 220
### 5.11.2 Develop Controls to Query Data using the LINQ Method ................ 222
## 5.12 Bind Data to Associated Controls in the Course Form ................ 223
## 5.13 Develop Controls to Query Data from the Course Form ................ 228
### 5.13.1 Query Data from the Course Table using the TableAdapter ................ 228
### 5.13.2 Query Data from the Course Table using the LINQ Method ................ 229

# PART II DATA QUERY WITH RUNTIME OBJECTS ................ 232

## 5.14 Introduction to Runtime Objects ................ 233
### 5.14.1 Procedure for Building a Data-Driven Application Using Runtime Objects ................ 234
## 5.15 Query Data using Runtime Object to SQL Server Databases ................ 235
### 5.15.1 Connect to SQL Server 2019 Express Databases............... 235
### 5.15.2 Create a New C# Project RTOSelect Project ................ 237
### 5.15.3 Query Data using the General Runtime Objects for the LogIn Form ................ 239
### 5.15.3.1 Coding Method 1: Using the DataAdapter to Query Data ................ 240
### 5.15.3.2 Coding Method 2: Using the DataReader to Query Data ................ 242
### 5.15.4 The Coding Process for the Selection Form ................ 244
### 5.15.5 Query Data using the General Runtime Objects for the Faculty Form ................ 245
### 5.15.6 Query Data using the General Runtime Objects for the Course Form ................ 250
- 5.15.6.1 Retrieve Data From Multiple Tables Using the Joined Tables Method................................ 251
- 5.15.6.2 Build the Codes for Two User-Defined Methods....................................... 256
## 5.16 Query Data Using Stored Procedures............................................................... 257
### 5.16.1 Create the Stored Procedure........................................................................... 258
### 5.16.2 Call the Stored Procedure............................................................................................... 259
### 5.16.3 Query Data Using Stored Procedures for Student Form.................................................. 260
### 5.16.4 Create a New C# SPSelect Project to Query Student Table............................................................................... 263
### 5.16.5 Query Data Using More Complex Stored Procedures....................................................... 272
### 5.16.6 Query Data Using Nested Stored Procedures.................................................................. 277
## 5.17 Query Data Using the LINQ to SQL Technique...................................................................... 280
### 5.17.1 Create a New C# Project and Setup LINQ to SQL Environment............................................................................................... 281
### 5.17.2 Create Entities and Class the DataContext to the Database......................................................... 283
### 5.17.3 Perform LINQ to SQL Query to Login Table via LogIn Form............................................... 285
### 5.17.4 Coding for the Selection Form........................................................................................... 289
### 5.17.5 Query Data Using the LINQ to SQL for the Faculty Form......................................................... 289
### 5.17.6 Query Data Using the Joined LINQ to SQL for the Course Form............................................................................................... 293
## 5.18 Query Data Using the LINQ to SQL Stored Procedures for the Student Form............................................................................... 297
## 5.19 Chapter Summary........................................................................................................... 302
## Homework......................................................................................................................... 304

# Chapter 6 Data Inserting with Visual C#................................................................ 309

## PART I INSERT DATA WITH VISUAL STUDIO.NET DESIGN TOOLS AND WIZARDS................................ 310
## 6.1 Insert Data into a Database........................................................................................... 310
### 6.1.1 Insert New Records into a Database Using the TableAdapter.Insert Method............................................................... 311
### 6.1.2 Insert New Records into a Database using the TableAdapter.Update Method............................................................... 311
## 6.2 Insert Data into the SQL Server Database using the InsertWizard Project............................................................................... 312
### 6.2.1 Create a New Project Based on the SelectWizard Project....................................................... 312
### 6.2.2 Application User Interfaces........................................................................................................... 312
### 6.2.3 Validate Data Before the Data Insertion........................................................................................... 312
- 6.2.3.1 The .NET Framework Classes............................................................................................... 313
- 6.2.3.2 Validate Data Using the Generic Collection........................................................................... 313
### 6.2.4 Validate Data After the Data Insertion........................................................................................... 316
### 6.2.5 Initialization Coding for the Data Insertion.................................................................................. 318
### 6.2.6 Build the Insert Query........................................................................................................................... 318
- 6.2.6.1 Configure the TableAdapter and Build the Data Insertion Query............................................................................................... 319
### 6.2.7 Develop Codes to Insert Data using the TableAdapter.Insert Method............................................................................... 320
- 6.2.7.1 Develop the Codes for Two User Defined Methods............................................... 322
### 6.2.8 Develop Codes to Insert Data Using the TableAdapter.Update Method............................................................................... 323
