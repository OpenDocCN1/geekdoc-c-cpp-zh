![](bbox=[0.111, 0.11, 0.705, 0.408])

FIGURE 2.19  Update function mapping.

The Delete stored procedures are similar to the update stored procedures in that they also need to implement optimistic locking and make sure that the deleted entity has not been modified since it was last retrieved from the database. However, because there are no new values to persist, their parameter lists are usually much shorter. Here is an example of the delete procedure for the Product entity:

```
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
```