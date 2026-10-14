# The ProductDB class

Figure 17-6 presents the C# code for the ProductDB class. To create this class, I used the Website→Add New Item command to add a class file to the App_Code folder. Then, I added the code for the public GetAllCategories and GetProductsByCategory methods. I also created a private method named GetConnectionString. This method is used by both of the public methods to retrieve the connection string for the Halloween database.

Before I explain the details of how these methods work, I want to point out the DataObject and DataObjectMethod attributes that appear in this class. These attributes are used to identify the class and methods as data objects, and you’ll learn how to use them in figure 17-10. For now, just realize that they’re used by the Data Source Configuration Wizard to determine which classes and methods to display when you configure an object data source.

The GetAllCategories method starts by creating a connection to the Halloween database. To get the connection for this database, it calls the GetConnectionString method. Next, this method creates a string that contains the Select statement that will be used to retrieve data from the Halloween database:

```
SELECT CategoryID, LongName
FROM Categories
ORDER BY LongName
```

Then, a SqlCommand object is created using the string that contains the Select statement and the connection object as parameters. Finally, the connection is opened, the ExecuteReader method of the command object is called to create a data reader object that contains the requested data, and the data reader is returned to the object data source.

The GetProductsByCategory method is slightly more complicated because it uses a parameter in its Select statement:

```
SELECT ProductID, Name, UnitPrice, OnHand
FROM Products
WHERE CategoryID = @CategoryID
ORDER BY ProductID
```

Here again, a SqlCommand object is created using this Select statement and the connection object. Then, a parameter named CategoryID is added to the command’s Parameters collection before the connection is opened, and the command is executed so it returns a data reader with the requested data.

The GetConnectionString method uses the ConfigurationManager class to retrieve the connection string named “HalloweenConnectionString” from the web.config file. As a result, the connection string for the Halloween database must be stored in this file. To refresh your memory about how to store it, please refer to figure 13-4 in chapter 13.