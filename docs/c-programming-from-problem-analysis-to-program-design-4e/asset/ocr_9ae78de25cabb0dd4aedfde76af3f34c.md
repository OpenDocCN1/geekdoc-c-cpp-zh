# 22. Write SQL statements for the following:

+   a. Retrieve all partNumber and partDescription columns from a Parts table that has 15 different columns.
+   b. Retrieve records from a Parts table for partNumbers 1000 through 2000. Display the partDescription only.
+   c. Insert a new record into a Customer table. Store the following values in the columns: LName=Osprey, FName=Teola, CNumber=23456. The columns are ordered as follows: CNumber, LName, FName.

23. What happens when you drag a dataset table from the Data Sources window onto a blank form?

24. How can you have controls (other than the default Data Sources window controls) display data from a database table?

25. How does a table adapter differ from a data adapter?

# PROGRAMMING EXERCISES

1. Create a small Family database with one table to include data about members of your family. Include data fields such as family member number, first name, last name, type of relationship, hometown, and age. You can be creative with the family member number or use the autoincremented number from the database. It must be a unique value; each member of your family must have a different family member number. Populate the database with members of your family. Be sure to include data about yourself in the table. Place at least 10 records in your database table, even if it is necessary to make up information. The type of database (SQL Server or Access) will be determined by your instructor. Write a C# program to display all of the data that appears in the database table on a data grid.

2. Using the database created in Programming Exercise 1, modify your solution to only display the names of the members of your family in a data grid. Dock the grid so that it fills the form. Change the color of the data grid columns, increase the size of the font, choose appropriate headings for your columns, and format the grid control so that it is professionally aesthetically appealing.

3. Using the database created in Programming Exercise 1, write a C# program to only display the names of the members of your family who are over 21 years of age. Display their name, age, and relationship to you. Provide an appropriate heading for the displayed items on the form and format the grid control.