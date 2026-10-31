But there's no solution without problems. A common complaint against O/R Mappers is that they are incapable of creating really good SQL code. Let's have a look at some examples that are often brought up. First is **UPDATE** with the **WHERE** clause. Look at the following example:

```
```sql
UPDATE Inventory
SET Balance = Balance - 1
WHERE Id = 42 AND Balance >= 1
```
```

This means that I only want to change the balance if there are products in stock. Otherwise, I do not want to change the balance. This is usually not supported directly by O/R Mappers. Instead, the approach that O/R Mappers would take here is to read the Inventory row with an optimistic lock, make the change, and write it back hoping for the best that there was no concurrency exception.

To clarify, here's an example of the optimistic approach (in this case as a SQL batch, but note that we aren't holding on to any locks because there is no explicit transaction, so this exemplifies the scenario):

```
```sql
--Remember the old Balance.
SET @oldBalance =
    (SELECT Balance
     FROM Inventory
     WHERE Id = 42)

--Calculate what the new Balance should be...

UPDATE Inventory
SET Balance = @newBalance
WHERE Id = 42 AND Balance = @oldBalance
--If @@ROWCOUNT now is 0, then the update failed!
```
```

Alternatively, it would read the Inventory row with a pessimistic lock, make the change, and write it back. Both approaches would cause scalability to suffer.

Another complaint about O/R Mappers is that they are often ineffective for updating large numbers of rows. The approach for updating all products via an O/R Mapper will probably be to read all products into a list, loop the list, and update the products one by one. If that could have been done with a single UPDATE statement instead, the throughput would have been tremendously better.

Yet another complaint is that it's hard to balance the amount to read. Either too little is read and there will therefore be lots of roundtrips when lazy loading, or more is read than is necessary. Type explosion is a common result from this, defining several variations of the type definitions.

But we can look at it the other way around as well. Can a person write all code extremely well and be consistent? And are all the developers on the team as good as the best one? Even if that's the case, should we use person hours for this if we get good enough performance with an automatic approach?

# Note