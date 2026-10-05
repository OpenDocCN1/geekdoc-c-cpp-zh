# How to work with parameters

After you create a parameter, you must add it to the Parameters collection of the command that will use the parameter. Because ADO.NET refers to SQL Server and Oracle parameters by name, you can add them to the Parameters collection in any sequence. In contrast, you must add OLE DB and ODBC parameters in the same order that they appear in the SQL statement since ADO.NET refers to them by position.

The first example in figure 20-5 shows how to use the Add method to add a parameter object to the Parameters collection. Here, the Parameters property of the command is used to refer to the Parameters collection. Then, the Add method of that collection is used to add the customerIDParm parameter that was created in the previous figure.

You can also use one of the overloaded Add methods to create a parameter and add it to the Parameters collection in a single statement. These methods let you specify a name and type or name, type, and size, and they return the parameter's created. That way, you can store the parameter in a variable so you can refer to it later if you need to.

Another way to create a parameter and add it to the Parameters collection is to use the AddWithValue method. This is illustrated in the second example in this figure, and this is the easiest way to create a parameter if you're not going to change its value. Like the Add methods, the AddWithValue method returns the parameter's created in case you don't create a variable to hold a parameter, you can refer to it later.

If you refer to the Parameters collection using either the parameter's name or its position as an indexer. This is illustrated in the third example in this figure. Here, the value of the @CustomerID parameter is set to the value of a variable named customerID.