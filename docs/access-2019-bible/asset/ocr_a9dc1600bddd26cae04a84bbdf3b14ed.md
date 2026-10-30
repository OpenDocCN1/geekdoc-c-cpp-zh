# All foreign key values must be matched by corresponding primary keys

The second referential integrity rule says that all foreign key values must be matched by corresponding primary keys. This means that every record in a table on the "many" (or child) side of a one-to-many relationship must have a corresponding record in the table on the "one" (or parent) side of the relationship. A record on the "many" side of a relationship without a corresponding record on the "one" side is said to be orphaned and is effectively removed from the database schema. Identifying orphaned records in a database can be very difficult, so you're better off avoiding the situation in the first place.

The second rule means the following:

+   - Rows cannot be added to a "many" side table (the child) if a corresponding record does not exist on the "one" side (the parent). If a child record contains a ParentID field, the ParentID value must match an existing record in the parent table.
+   - The primary key value in a "one" side table cannot be changed if the change would create orphaned child records.
+   - Deleting a row on the "one" side must not orphan corresponding records on the "many" side.

For example, in the sales example, the foreign key in each record in tblSales (the "many" side) must match a primary key in tblCustomers. You can't delete a record in tblCustomers (the "one" side) without deleting the corresponding records in tblSales.

One of the curious results of the rules of referential integrity is that it's entirely possible to have a parent record that isn't matched by any child records. Intuitively, this makes sense. A company may certainly have employees who haven't yet been issued paychecks. Or the Collectible Mini Cars company may hire a new employee who hasn't made any sales yet. Eventually, of course, most parent records are matched by one or more child records, but this condition is not a requirement of relational databases.

As you'll see in the next section, Access makes it easy to specify the integrity rules you want to employ in your applications. You should be aware, however, that not using the referential integrity rules means that you might end up with orphaned records and other data integrity problems.

# Keys

When you create database tables, like those created in Chapter 3, you should assign each table a primary key. This key is a way to make sure that the table records contain only one unique value; for example, you may have several contacts named Michael Heinrich, and you