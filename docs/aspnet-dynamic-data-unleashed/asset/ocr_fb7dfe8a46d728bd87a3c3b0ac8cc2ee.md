When you run this code, you might notice that the second user (represented by context2) submits the changes last and the changes made by the first user are lost.

To prevent data loss, database applications have traditionally relied on record locking. When a user starts editing a particular record, the application would lock it, preventing others from modifying it at the same time. This approach works better when the number of users is small and the number of records is large, thus reducing the chance of contention. However, physical locking can prevent other users not only from changing but also from reading the locked records. This can lead to significant performance degradation and is generally considered a bad practice.

The Entity Framework has built-in support for an alternative strategy, called Optimistic Concurrency Control. When saving modified entities, the ObjectContext generates UPDATE statements with a WHERE clause that ensures that changes are made only if the entity has not changed since the last time it was retrieved from the database. In other words, the framework assumes that chances of contention are low and, optimistically, allows you to modify the entity without locking the record. If somebody else modified the same record in the meantime, you simply get an exception when calling the SaveChanges method.

To take advantage of the optimistic concurrency support, first you need to modify the definitions of the properties in the Entity Designer to set their Concurrency Mode values to Fixed, as shown in Figure 2.8. You need to do this for all properties you want the Entity Framework to check for modifications before saving the entity.

![](bbox=[0.15, 0.55, 0.45, 0.85])

FIGURE 2.8 Setting Property Concurrency Mode.

When the model has been modified, calling the SaveChanges for context1 in the previous code example generates the following SQL statement:

```
```sql
exec sp_executesql N'update [dbo].[Products]
set [UnitsInStock] = @0
where (([ProductID] = @1) and ([UnitsInStock] = @2))'
,'N'@0 smallint,@1 int,@2 smallint','@0=50,@1=1,@2=20
```
```