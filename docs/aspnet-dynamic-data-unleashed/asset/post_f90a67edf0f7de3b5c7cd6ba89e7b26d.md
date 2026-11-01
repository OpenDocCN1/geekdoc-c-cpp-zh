
![](img/11b373b78859e17d318fd76939a0df9d_95_0.png)

## FIGURE 2.16 Add function import.

When you click the OK button in the Add Function Import dialog, the function import is added to the conceptual section of the model. You can find it under Entity Container/Function Imports in the model browser; Figure 2.17 shows an example.

![](img/11b373b78859e17d318fd76939a0df9d_95_1.png)

## FIGURE 2.17 Function import in the conceptual section of model browser.

For each function import, the Entity Designer generates a strongly-typed method in the ObjectContext class. Following is an example of using the newly added GetProductsToReorder method to list all products returned by the stored procedure:

```
using (NorthwindEntities context = new NorthwindEntities())
{
    IEnumerable<Product> products = context.GetProductsToReorder();
    foreach (Product p in products)
        Console.WriteLine(p.ProductName);
}
```

The generated method returns an IEnumerable and not an IQueryable. Although you can use the familiar LINQ operators to manipulate it further, keep in mind that these operations are performed in the application memory and not by the database server. Instead, it is often best to modify the definition of the stored procedure itself and have it return a more focused result set.

## Insert, Update, and Delete Stored Procedures

The Entity Framework also allows you to use stored procedures to perform insert, update, and delete operations instead of generating SQL statements dynamically. When combined with restriction of the application permissions to only read data, this technique can help reduce accidental data corruption and locking due to casual browsing, when developers or administrators use a tool, such as SQL Server Management Studio to interactively explore live data in a production system.

Here's an example of the stored procedure that inserts a new Product entity into the Products table:

```
CREATE PROCEDURE [dbo].[Products_Insert]
@ProductName nvarchar(40), @SupplierID int,
@QuantityPerUnit nvarchar(20), @UnitPrice money, @UnitsInStock smallint,
@UnitsOnOrder smallint, @ReorderLevel smallint, @Discontinued bit
AS
BEGIN
    INSERT INTO Products
    (ProductName, SupplierID, CategoryID,
    QuantityPerUnit, UnitPrice, UnitsInStock,
    UnitsOnOrder, ReorderLevel, Discontinued)
    VALUES
    (@ProductName, @SupplierID, @CategoryID,
    @QuantityPerUnit, @UnitPrice, @UnitsInStock,
    @UnitsOnOrder, @ReorderLevel, @Discontinued);
    
    SELECT SCOPE_IDENTITY() as ProductID;
END
```

Notice that this stored procedure takes a set of parameters, each representing a particular table column, such as ProductName and SupplierID. The stored procedure performs the INSERT statement and a SELECT statement to return the ProductID value of the newly inserted row.

For the Entity Framework to take advantage of this stored procedure, it needs to be added to the storage section of the entity model, similar to the GetProductsToReorder stored procedure discussed earlier. However, instead of adding it as a function import to the conceptual model, right-click the Product entity in the Entity Designer and select Stored Procedure Mapping from the context menu. You will see the Mapping Details window similar to that shown in Figure 2.18.

![](img/11b373b78859e17d318fd76939a0df9d_97_0.png)

FIGURE 2.18 Insert function mapping.

The Functions tab of the Mapping window allows you to map the stored procedure parameters (shown on the left) to the entity properties (shown on the right). In this example, the generated ProductID value is mapped in the Result Column Bindings section.

The Update stored procedures are somewhat more complex because they need to implement the optimistic locking normally performed by the Entity Framework. In addition to the primary key value required to uniquely identify the target row and the current values of all fields, the update procedure needs to provide a separate parameter for each entity property that has Concurrency Mode set to Fixed in the entity model. In the following example, the Products_Update procedure provides a separate set of parameters for all properties, one set for the new values, used to update the row, and the other set of old values, used to make sure that the entity has not been modified since it was last retrieved from the database.

The update stored procedure also needs to be added to the model and used to map the Product entity as shown in Figure 2.19. Each property of the Product entity is mapped twice—first to the parameter that receives the “old” value of the entity property as it was originally retrieved from the database and then to the parameter that receives the “new” value that needs to be persisted. Notice that the @RowsAffected output parameter of the stored procedure, which returns the number of rows actually modified by the stored procedure, has a checkbox in the Rows Affected Parameter column. This parameter is used by the Entity Framework to determine if the optimistic locking was performed successfully and throw the OptimisticConcurrencyException if it returns zero.

![](img/11b373b78859e17d318fd76939a0df9d_99_0.png)

FIGURE 2.19 Update function mapping.

The Delete stored procedures are similar to the update stored procedures in that they also need to implement optimistic locking and make sure that the deleted entity has not been modified since it was last retrieved from the database. However, because there are no new values to persist, their parameter lists are usually much shorter. Here is an example of the delete procedure for the Product entity:

```sql
CREATE PROCEDURE [dbo].[Products_Delete]
    @ProductID int, @ProductName nvarchar(40), @SupplierID int, @CategoryID int,
    @QuantityPerUnit nvarchar(20), @UnitPrice money, @UnitsInStock smallint,
    @UnitsOnOrder smallint, @ReorderLevel smallint, @Discontinued bit,
    @RowsAffected int out
AS
BEGIN
    DELETE FROM Products
    WHERE
        ProductID = @ProductID AND
        SupplierID = @SupplierID AND
        CategoryID = @CategoryID AND
        QuantityPerUnit = @QuantityPerUnit AND
        UnitPrice = @UnitPrice AND
        UnitsInStock = @UnitsInStock AND
        UnitsOnOrder = @UnitsOnOrder AND
        ReorderLevel = @ReorderLevel AND
        Discontinued = @Discontinued;

    SET @RowsAffected = @@ROWCOUNT
END
```

The Entity Framework is optimized for rich-client applications that retrieve and manipulate a relatively small number of records at a time. However, by turning off the object tracking options, its performance can be improved for multi-threaded web applications as well as applications working with a large number of records in batch mode. Although the Entity Framework generates high-quality, parameterized SQL code appropriate for most common data access scenarios, it also allows the use of stored procedures to create, read, update, and delete entities/database records.

Entity Framework supports the TransactionScope class from the System.Transactions namespace and optimistic concurrency for conflict detection in multi-user scenarios. It does not support pessimistic locking out of the box; however, implementing it is possible with the help of custom stored procedures.

The Entity Framework represents a long-term strategic investment for Microsoft. As of .NET version 4, it is a powerful framework appropriate for use on most enterprise application projects. It offers significant productivity improvements compared to the classic ADO.NET and has become a recommended choice with some of the new technologies developed by Microsoft, including ASP.NET Dynamic Data. The Entity Framework is under active development. Version 4.1 added support for Code-First approach, making it possible to define entity model directly in application code, as classes. The upcoming version 4.5 will bring significant enhancements to the Entity Designer, including support for enumerated types and multiple diagrams, making developers using the database-first approach, discussed in this chapter, as well as the model-first approach, much more productive.
