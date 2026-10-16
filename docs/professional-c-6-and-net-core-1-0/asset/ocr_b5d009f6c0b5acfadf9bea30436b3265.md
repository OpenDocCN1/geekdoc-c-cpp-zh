```
}; 
context.Menus.Add(mInvalid);
records = await context.SaveChangesAsync();
WriteLine($"{records} records added");
tx.Commit();
}
catch (DbUpdateException ex)
{
WriteLine($"{ex.Message}");
WriteLine($"{ex?.InnerException.Message}");
WriteLine("rolling back...");
tx.Rollback();
}
WriteLine();

```

When you run the application, you can see that no records have been added, although the SaveChangesAsync method was invoked multiple times. The first return of SaveChangesAsync lists one record as being added, but this record is removed based on the Rollback later on. Depending on the setting of the isolation level, the updated record can only be seen before the rollback was done within the transaction, but not outside the transaction.

```
TwoSaveChangesWithOneTxAsync
1 records added
An error occurred while updating the entries. See the inner exception for details.
The INSERT statement conflicted with the FOREIGN KEY constraint"FK_Menu_MenuCard_MenuCardId".
The conflict occurred in database 'MenuCards',
table"mc.MenuCards", column 'MenuCardId'.
rolling back...
```

> NOTE With the BeginTransactionAsync method, you can also supply a value for the isolation level to specify the isolation requirements and locks needed in the database. Isolation levels are discussed in Chapter 37.

# Summary

This chapter introduced you to the features of the Entity Framework Core. You’ve learned how the object context keeps knowledge about entities retrieved and updated, and how changes can be written to the database. You’ve also seen how migrations can be used to create and change the database schema from C# code. To define the schema, you’ve seen how the database mapping can be done using data annotations, and you’ve also seen the fluent API that offers more features compared to the annotations.

You’ve seen possibilities for reacting to conflicts when multiple users