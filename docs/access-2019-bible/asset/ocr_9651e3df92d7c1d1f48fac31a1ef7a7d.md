```
Set db = CurrentDb

sSQL = "SELECT DISTINCTROW OrderDetails.OrderID, " _
& "OrderDetails.ProductID, " _
& "Products.ProductName, " _
& "OrderDetails.UnitPrice, " _
& "OrderDetails.Quantity, " _
& "OrderDetails.Discount, " _
& "CCur(OrderDetails.UnitPrice*Quantity) AS ExtendedPrice " _
& "FROM Products INNER JOIN OrderDetails " _
& "ON Products.ProductID = OrderDetails.ProductID " _
& "ORDER BY OrderDetails.OrderID;"

Debug.Print "sSQL: " & sSQL

Set rs = db.OpenRecordset(sSQL, DB_OPEN_DYNASET)

rs.Close
Set rs = Nothing
Set db = Nothing

End Sub
```

Unlike the MsgBox statement, you don’t have to do anything special to suppress the Debug.Print output from the user interface. The output of Debug.Print only goes to the Immediate window, and because end users never see the Immediate window, you don’t have to worry about a user encountering debug messages.

The problems with Debug.Print are obvious from Figure 27.5. Long strings don’t wrap in the Immediate window. Also, the Immediate window must be visible in order for you to view its output. But these limitations are relatively harmless, and you’ll frequently use Debug.Print in your applications.

> NOTE
> Some people have reported that excessive numbers of Debug.Print statements can slow an application. Even though the Immediate window is not visible, Access executes the Debug.Print statements that it finds in its code. You may want to consider surrounding each Debug.Print statement with the compiler directives described in the "Compiler Directives" sidebar to remove them from the end user’s copy of the application.

# Using the Access Debugging Tools

Access features a full complement of debugging tools and other capabilities. You use these tools to monitor the execution of your VBA code, halt code execution on a statement so that you can examine the value of variables at that moment in time, and perform other debugging tasks.