data. You can simplify the code in a Web page by enabling the LinqDataSource control to automatically create the commands for interacting with the data. The LinqDataSource control is similar to the SqlDataSource and ObjectDataSource controls in the respect that it can be used to declaratively bind other ASP.NET controls on a page to a data source. The difference is that instead of binding directly to a database or to a generic class, the LinqDataSource control is designed to bind a data model that is LINQ enabled.

The LinqDataSource control cannot be directly connected to a database. Instead, you interact with entity classes that represent the database and the tables. You can generate the entity classes by using the Object Relational Designer or by running the SqlMetal.exe utility and then connect the LinqDataSource control to a database by setting the ContextTypeName property to the name of the class that represents the database. You can set the TableName property to the name of the class that represents the data table for connecting to a particular table in the database. For example, to connect to the Employees table of the Northwind database, you can set the ContextTypeName property to the Northwind and the TableName property to the Employees table. Similarly, for retrieving data from an in-memory data collection, you can set the ContextTypeName property to the object that contains the data collection. You can set the TableName property in this case to the property or the field that returns the data collection.

> NOTE
> You have learned about the LinqDataSource control in detail in Chapter 26: Data Binding in ASP.NET Applications of the book. The noteworthy properties, methods, and events of the control are listed in the Chapter 26.

# Extension Methods

The extension() method in .NET Framework allows you to add methods to existing types without creating a new derived type. This is done by recompiling and modifying the original type. The extension() method takes parameters in which the first parameter defines the types that it extends. The basic difference between an extension() method and a normal static() method is that an extension() method requires this keyword with the first parameter. You must note that the extension() method cannot access the private members of the type that it extends.

The class that defines the LINQ extension method is the Enumerable class, which is contained in the System.Linq namespace. To use the extension() method, you just need to import this namespace that is contained in the System.Core assembly. You can use the Where(), OrderByDescending(), and Select() methods from the Enumerable class. Each of these methods returns the IEnumerable<TSource> method.

The extension() method is a useful concept, especially in the cases when you want to extend a class that you cannot, such as a sealed class or a class for which you do not have source code.

# Anonymous Methods

Anonymous methods allow you to handle an event rather than having a separate event handler. For example, if you want to display a message box at the click of a button, you can handle it in a standard way with a delegate and an event handler or you can also perform the action using an anonymous method. To put it simply, an anonymous method is a block of code used as a parameter for the delegate. The main benefit of using anonymous method is to reduce the code that you need to write. When you are using the anonymous method, you do not need to define any static event handler. The anonymous method is defined at the time the caller is handling the event.

You should always keep a few points in mind when using an anonymous method, which are as follows:

+   - You cannot have a Jump statement, Break, GoTo, or Continue, in an anonymous method that has a target outside the anonymous method.

+   - You should also not use an unsafe code inside an anonymous method.

+   - If you need to write the same functionality more than once, you should not use an anonymous method.

The anonymous methods were introduced in .NET Framework 2.0 but .NET Framework 3.5 offers a new syntax for the anonymous method called the Lambda expression. Instead of passing anonymous methods, you can do the same job in LINQ by using the Lambda expression.