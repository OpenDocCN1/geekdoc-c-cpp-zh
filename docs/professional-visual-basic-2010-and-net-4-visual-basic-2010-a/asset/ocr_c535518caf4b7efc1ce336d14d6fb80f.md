# Creating the Product Object

For this example, you will work with the Titles table from the pubs database, which means you need to create a titles table that will use LINQ to SQL to map to this table. Accomplishing this task is simply a matter of opening a view of the tables contained within the database from the Server Explorer dialog within Visual Studio and dragging and dropping the Titles table onto the left-hand design surface of the O/R Designer. The results of this action are illustrated in Figure 10-8.

![](bbox=[0.7, 0.08, 0.88, 0.26])

With this action, a bunch of code is added to the designer files of the .dbml file on your behalf. These classes give you strongly typed access to the titles table. For a demonstration of this, turn your attention to the console application’s Main.vb file. Following is the code required for this example:

```
Module Main
    Sub Main()
        Dim dc As New pubsDataContext
        Dim query = dc.titles
        For Each item In query
            Console.WriteLine("{0}: {1}",
                item.title_id, item.title)
        Next
        Console.WriteLine("Press ENTER to exit")
        Console.ReadLine()
    End Sub
End Module
```

Code snippet from LinqReading Project

This short bit of code is querying the Titles table within the pubs database and pulling out the data to display. It is useful to step through this code starting with the first line in the Main method:

```
Dim dc As New pubsDataContext()
```

The pubsDataContext object is an object of type DataContext. You can view this as a class that maps to a Connection type object. This object works with the connection string and connects to the database for any required operations.

The next line is quite interesting:

```
Dim query = dc.titles
```

Here, you are using an implicitly typed variable. If you are unsure of the output type, you can assign a type to the query variable and the type will be set into place at compile time. Actually, the code dc.titles returns a System.Data.Linq.Table(Of LinqReading.titles) object, and this is what the query type is set as, when the application is compiled. Therefore, you could have also just as easily written the statement as follows:

```
Dim query As Table(Of title) = dc.titles
```

This approach is actually better because programmers who look at the application’s code later will find it easier to understand what is happening, as just using the Dim query by itself has so much of a hidden aspect to it. To use Table(Of title), which is basically a generic list of Title objects, you should make a reference to the System.Data.Linq namespace (using Imports System.Data.Linq).

The value assigned to the Query object is the value of the titles property, which is of type Table(Of title). From there, the next bit of code iterates through the collection of Title objects found in Table(Of title):

```
For Each item In query
    Console.WriteLine("{0}: {1}",
        item.title_ID, item.title)
Next
```