# Part 1

Create a form named DisplayRentals that lets the user display Rental records, one at a time, as shown below.

![](bbox=[0.035, 0.145, 0.52, 0.455])

Note: If the version of SQL Server you use is incompatible with the database, when you create the data source, you will be asked whether you want to update the database. Answer “Yes.” Again, make sure that you answer “No” when the DataSource Configuration Wizard asks you whether you want to copy the database to the project folder. (If you answer “Yes,” the changes you make to the table will be lost the next time you run the project.)

The primary key, RentalId, is an auto-increment field. To view the fields and their properties, right click Rental table in Server Explorer window, and select Open Table Definition. The T-SQL window displays the SQL that creates the table. The key word IDENTITY(1,1) specifies that RentalId is an auto-increment field that increments by 1, starting with 1.

To view the data tables, open RentalDataSet.xsd. Select RentalId field and view its properties. Make sure that the auto-increment properties are set as follows:

![](bbox=[0.035, 0.69, 0.46, 0.83])