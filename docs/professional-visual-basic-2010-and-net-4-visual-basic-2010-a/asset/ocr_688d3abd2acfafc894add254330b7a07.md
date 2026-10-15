As shown in Chapter 9, you create the XmlReader using the shared Create method. This method has a number of overridden versions. In this case, the string version of the URL is used to create the XmlReader. The code then loops through the resulting XML until the start element for the Latitude element is found. As you know, the two values are next to each other; the code may then access them and stop reading. Figure 12-26 shows this new function in SQL Server Management Studio.

![](bbox=[0.09, 0.18, 0.65, 0.46])

FIGURE 12-26

# Using the User-Defined Function

Even though the fnGetLocation function is written in Visual Basic, you can still use this function from T-SQL. This means that you can use either Visual Basic or T-SQL for a given SQL Server object, whichever is better suited to the scenario. The following code shows the procedure used to insert new stores. This procedure is written in T-SQL, but it calls the function written in Visual Basic. Alternately, you could create an insert trigger that calls the function to determine the store’s location.

```
CREATE PROCEDURE dbo.procInsertStore
(
    @name nvarchar(50),
    @street nvarchar(512),
    @city nvarchar(50),
    @state char(2),
    @zip varchar(50)
)
AS
    /* need to populate location */
    DECLARE @loc AS Location;
    SET @loc = dbo.fnGetLocation(@street, @city, @state, @zip);
    INSERT INTO Stores (Name, Street, City, State, Zip, GeoLocation)
        OUTPUT INSERTED.id
    VALUES (@name, @street, @city, @state, @zip, @loc);
    RETURN @@IDENTITY
```

Code snippet from FooStore

The stored procedure uses the function and user-defined type just as it would use the same objects written in T-SQL. Before storing the store data, it calls the Web service to determine the latitude and longitude of the location, and then stores the data in the table.

We are now ready to add data to the three tables. Add a few stores (see Figure 12-27) using the stored procedure. The actual data is not that important, but having multiple stores relatively close to one another will be useful later.