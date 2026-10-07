
# Contents

xiii

- 6.3 Insert Data into the Course Table with Three Methods............................................... 329
- 6.3.1 Add Class Variables and Modify the Codes in the Form_Load() Method....................................... 329
- 6.3.2 Build the Query Method InsertCourse()................................................................ 330
- 6.3.3 Create the Stored Procedure Using the TableDataAdapterQuery Configuration Wizard....................................... 331
- 6.3.4 Build the Codes for the Insert Button's Click Method........................................... 332
- 6.3.5 Build the Codes for User-Defined Methods............................................................... 334

# PART II DATA INSERTION WITH RUNTIME OBJECTS................................................ 338

- 6.4 The General Runtime Objects Method.................................................................. 339
- 6.5 Insert Data into the SQL Server Database using the Runtime Object Method... 340
- 6.5.1 The Coding Process for the Data Validation before the Data Insertion..................................... 341
- 6.5.2 The Coding Process for the Data Validation after the Data Insertion......................................... 342
- 6.5.3 The Coding Process for the Data Insertion Action........................................ 343
- 6.6 Insert Data into the SQL Server Database Using Stored Procedures.................. 349
- 6.6.1 Develop Stored Procedures of SQL Server Database............................... 350
- 6.6.2 Develop Codes to Call Stored Procedures to Insert Data to the Course Table....................................... 352
- 6.6.2.1 Validate the Data before the Data Insertion..................................... 353
- 6.6.2.2 Build the Codes for the Insert Click Method to Perform Insertion....................................... 353
- 6.6.2.3 Validate Data Insertion after the Course Data Insertion............................................... 356
- 6.7 Chapter Summary.................................................................................. 357
- Homework.................................................................................................. 358

# Chapter 7 Updating and Deleting with Visual C#.NET ....................... 363

## PART I DATA UPDATING AND DELETING WITH VISUAL STUDIO DESIGN TOOLS AND WIZARDS.................................................. 364

- 7.1 Update or Delete Data against SQL Server Databases....................... 364
- 7.1.1 Updating and Deleting Data against Related Tables in a DataSet............................... 364
- 7.1.2 Update or Delete Data against Database Using TableAdapterDBConnect Methods................................................ 365
- 7.1.3 Update or Delete Data against Database Using TableAdapter.Update Method....................... 365
- 7.2 Update and Delete Data for the Faculty Table in our SQL Server Database................................ 366
- 7.2.1 Configure the TableAdapter and Build the Data Updating and Deleting Queries................................................ 367
- 7.2.2 Develop Codes to Update Data Using the TableAdapterDBDirect Method....................... 369
- 7.2.2.1 The Codes Modifications............................................... 369
- 7.2.2.2 The Codes Creations............................................... 370
- 7.2.3 Develop Codes to Update Data Using the TableAdapter.Update Method................................................ 371
- 7.2.4 Develop Codes to Delete Data Using the TableAdapterDBDirect Method....................................... 372
- 7.2.5 Develop Codes to Delete Data Using the TableAdapter.Update Method........................................................... 374
- 7.2.6 Run Project to Validate the Data after the Data Updating and Deleting................................................................ 374

## PART II DATA UPDATING AND DELETING WITH RUNTIME OBJECTS............................... 377

- 7.3 The Run Time Method Method................................................................................................ 378
- 7.4 Update and Delete Data Using the Run Time Object Method................................................................ 379
- 7.4.1 Update Data for the Faculty Table in the SQL Server Database............................................... 379
- 7.4.1.1 Develop Codes to Update Data.................................................................................. 380
- 7.4.1.2 Validate the Data Updating......................................................................................... 381
- 7.4.2 Delete Data from the Faculty Table for the SQL Server Database.......................................... 381
- 7.4.2.1 Develop Codes to Delete Data............................................................................... 381
- 7.4.2.2 Validate the Data Updating..................................................................................... 383
- 7.4.3 Update Data for the Course Table in the SQL Server Database......................................................... 386
- 7.4.3.1 Develop Codes to the Course Record............................................................................... 386
- 7.4.3.2 Validate the Data Updating..................................................................................... 388
- 7.4.4 Delete Data for the Course Table in the SQL Server Database......................................................... 389
- 7.4.4.1 Develop Codes to the Course Record............................................................................... 389
- 7.4.4.2 Validate the Course Updating............................................................................... 391
- 7.5 Update and Delete Data from the Database Using Stored Procedures............................................... 392
- 7.5.1 Update and Delete Data against SQL Server Database Using Stored Procedures................................................ 392
- 7.5.1.1 Modify an Existing Project to Create Our New Project................................................ 392
- 7.5.1.2 Develop Stored Procedures with the Server Explorer Window................................................ 395
- 7.5.1.3 Call the Stored Procedures to Perform Data Updating and Actions................................................ 397
- 7.6 Update and Delete Data against Databases Using the LINQ to SQL Query............................................... 399
- 7.6.1 Modify the Codes for the Faculty Form............................................................... 400
- 7.6.2 Build the User-Defined Method (Faculty) with SQL Method................................................ 401
- 7.6.3 Develop the Codes for the Delete Button Click Method............................................................... 401
- 7.6.4 Develop the Codes for the Delete Button Method............................................................... 403
- 7.7 Chapter Summary.................................................................................. 406
- Homework.................................................................................................. 407

# Chapter 8 Accessing Data in ASP.NET ............................................................................ 411

- 8.1 Historical Review for ASP.NET Framework................................................................ 411
- 8.2 What is .NET Framework?............................................................................... 412
- 8.3 What is ASP.NET and ASP.NET Framework?................................................................ 413
- 8.3.1 ASP.NET Web Application Structure............................................................................... 415
- 8.3.2 ASP.NET Execution Model............................................................................... 416
- 8.3.3 What Really Happens When a Web Application Executed................................................................ 416
- 8.3.4 The Requirements to Test and Run a Web Project................................................................ 417
- 8.3.5 Install Missing Component to Get ASP.NET Template for .NET Framework................................................................ 418
- 8.4 Develop ASP.NET Web Application to Select Data from SQL Server Databases................................................................................ 419
- 8.4.1 Create the User Interface – Login Form............................................................................... 420
- 8.4.2 Develop the Codes to Access and Select Data from the Database............................................................................... 422
- 8.4.3 Validate the Data in the Client Side............................................................................... 425
- 8.4.4 Select a Web Browser to Effectively Run Our Web Project.......................................................................... 427
- 8.4.5 Create the Second User Interface – Selection Page............................................................................... 427
- 8.4.6 Develop the Codes for the Selection Page to Open the Other Page............................................................................... 430
- 8.4.7 Create the Third User Interface – Faculty Page............................................................................... 432
- 8.4.8 Develop the Codes to Select the Desired Faculty Information............................................................................... 433
- 8.4.8.1 Develop the Codes for the Page_Load Method................................................................
- 8.4.8.2 Develop the Codes for the Select Button Method.................................................................. 434
- 8.4.8.3 Develop the Codes for Other Methods............................................................................... 435
- 8.4.9 Create the Fourth User Interface – Course Page......................................................................... 437
- 8.4.9.1 The AutoPostBack Property of the List Box Control....................................................... 438
- 8.4.9.2 Develop the Codes to Select the Desired Course Information............................................................................... 439
- 8.4.9.3 Coding for the Course Page Loading and Ending Methods............................................................................... 440
- 8.4.9.4 Coding for the Select Button Click Method......................................................................... 441
- 8.4.9.5 Coding for the SelectedIndexChanged Method of the List Control............................................................... 443
- 8.4.9.6 Coding for the User-Defined Method FullCourseReaderTextBox().......................................................................... 444
- 8.5 Develop ASP.NET Web Application to Insert Data Into SQL Server Databases............................................................................... 446
- 8.5.1 Develop the Codes to Insert a New Record into the Faculty Table............................................................................... 446
- 8.5.2 Develop the Codes for the Page_Load Method............................................................................... 447
- 8.5.3 Develop the Codes for the Insert Button Click Method............................................................................... 448
- 8.5.4 Develop the Codes for Other Methods............................................................................... 449
- 8.5.5 Validate the Insertion............................................................................... 451
- 8.6 Develop Web Applications to Update and Delete Data in SQL Server Databases............................................................................... 452
- 8.6.1 Develop the Codes for the Update Button Click Method......................................................................... 453
- 8.6.2 Develop the Codes for the Delete Button Method............................................................................... 456
- 8.6.2.1 Relationships between Five Tables in Our Sample Database............................................................................... 457
- 8.6.2.2 Data Deleting Order Sequence............................................................................... 458
- 8.6.2.3 Use the Cascading Delete Option to Simplify the Data Deleting Actions............................................................................... 458
- 8.6.2.4 Develop the Codes to Perform the Data Deleting Action............................................................................... 460
- 8.7 Develop ASP.NET Web Applications with LINQ to SQL Query............................................................................... 462
- 8.7.1 Create Entity Classes and Connect the DataContext to the Database............................................................................... 463
- 8.7.2 Perform LINQ to SQL Query to Login Table via Page............................................................................... 464
