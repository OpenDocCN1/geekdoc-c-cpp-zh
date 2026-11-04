and memory. In contrast, the database itself has great tools for finding specific records, particularly if the table uses the Name field as an index. In that case, the database may need to perform only a few disk accesses to search through its index structure for the right customer, a much more efficient operation than moving 100,000 records into the program and then searching them sequentially.

For many reasonably simple queries, the translation from LINQ query syntax into something the database can understand works and there's no problem. Sometimes, however, your query code doesn't translate easily into database speak and the database can't execute it.

For example, the following code shows how the Find Customer program described in Lesson 36 displayed customers who owe more than $50 and who are more than 30 days overdue. (In this code the variable today holds the current date and is used to simplify the code.)

```
// Display customers who owe at least $50
// and are overdue at least 30 days.
var overdueQuery =
    from Customer cust in customers
    where (cust.Balance <= -50) &&
          (today.Subtract(cust.DueDate).TotalDays > 30)
    select cust;
overdueListBox.DataSource = overdueQuery.ToList<Customer>();
```

Unfortunately, SQL Server doesn't have a function that subtracts one date from another, so this query doesn't translate perfectly into database commands and at run time the program throws the following exception:

```
Method 'System.TimeSpan Subtract(System.DateTime)' has no supported translation to SQL.
```

One solution is to rewrite the query in terms that the database can understand. The following code shows a query that LINQ to SQL can translate successfully:

```
// Display customers who owe at least $50
// and are overdue at least 30 days.
var overdueQuery =
    from Customer cust in db.Customers
    where (cust.Balance == null || cust.Balance.Value < -50) &&
          (cust.DueDate == null || today > cust.DueDate.Value.AddDays(30))
    //orderby cust.Balance ascending, cust.FirstName
    select String.Format("{0} {1}\t{2:C}\t{3:d}",
        cust.FirstName,
        cust.LastName,
        cust.Balance, cust.DueDate);
overdueListBox.DataSource = overdueQuery.ToArray();
```

Although the translation to database code doesn't know how to subtract dates, it does know how to add days to a date so this query uses that capability. It selects records where the customer:

+   - Has no balance or has a balance less than $50, and
+   - Has no due date or today's date is greater than the due date plus 30 days