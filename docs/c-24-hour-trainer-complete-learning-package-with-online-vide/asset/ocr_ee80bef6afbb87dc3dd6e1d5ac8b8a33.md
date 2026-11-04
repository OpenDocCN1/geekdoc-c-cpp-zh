The partial keyword indicates that this class is part of a class that may have pieces elsewhere. In this case, it means the `ToString` method should be added to the `Customer` class built by LINQ to SQL so you don't need to modify the automatically generated code.

+   c. Declare a field named `Db` with your `DataContext` class's type.
+   d. Write a `LoadData` method that queries the database and sets the `ListBox`'s `DataSource` property to the result.
+   e. In the form's `Load` event handler, initialize the `Db` variable and call `LoadData`.

3. Copy the program you built for Exercise 2 and make it display the currently selected customer's properties. To do that:

+   a. Write a `ShowSelectedCustomer` method. It should get the `ListBox`'s `SelectedItem` property as a `Customer` object. It should then display the object's properties in the `TextBoxes`.
+   b. In the `ListBox`'s `SelectedIndexChanged` event handler, call `ShowSelectedCustomer`.

4. Copy the program you built for Exercise 3 and make it update the `Customer` objects when the user modifies the balance or due date. To do that, give the `TextBoxes` `TextChanged` event handlers. They should get the current `Customer` object, parse the value in the `TextBox`, and save the value in the `Customer` object. Use a try catch statement to protect against invalid data and, if a value is invalid, store `null` in the object.

5. Copy the program you built for Exercise 4 and finish it by making the Save and Cancel buttons work. To do that:

+   a. Make the Save button call `Db.SubmitChanges()`. That saves any changes pending in the `DataContext` back to the SQL Server database.
+   b. Make the Cancel button execute the following statement to cancel any changes pending in the `DataContext`:

```
Db.Refresh(System.Data.Linq.RefreshMode.OverwriteCurrentValues, customerListBox.Items);
```

Then make the button's event handler call `ShowSelectedCustomer` to redisplay the currently selected customer.

> **NOTE** Please select the videos for Lesson 37 online at www.wrox.com/go/csharp24hourtrainer2videos.