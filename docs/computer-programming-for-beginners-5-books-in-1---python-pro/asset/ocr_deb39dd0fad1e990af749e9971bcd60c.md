the time, you'll be dealing with query specifications. Query expressions are SQL expressions that start with SELECT and contain different elements. To keep it simple, let's assume that SELECT is a query specification. Database products also use this assumption, so it is certainly effective.

You can't summarize, combine, or automatically delete the information inside the view.

The table you're working with should have at least one updateable column.

Every column inside the view should point to a single column in a table.

Every row inside the view should point to a single row in a table.

# How to Drop a View

In some cases, you need to delete a view from a database. To do that, you need to use the following syntax:

```
DROP VIEW (name of the view);
```

The system will delete the view as soon as you run this statement. However, the process won't affect the underlying information (i.e. the data stored inside the actual tables). After dropping a view, you may recreate it or use its name to generate another view. Let's analyze a basic example:

```
DROP VIEW BOOK_PUBLISHERS;
```

This command will delete the BOOK_PUBLISHERS view from the database. However, the underlying information will be unaffected.

# Database Security

Security is an important element of every database. You need to make sure that your database is safe from unauthorized users who may view or alter data. Meanwhile, you also need to ensure that authorized users can access and/or change data without any problems. The best solution for this problem is to provide each user with the privileges they need to do their job.

To protect databases, SQL has a security scheme that lets you specify which database users can view specific information from. This scheme also allows you to set what actions each user can perform. This security scheme (or model) relies on authorization identifiers. As you've learned in the second chapter, authorization identifiers are objects that represent one or more users that can access/modify the information inside the database.