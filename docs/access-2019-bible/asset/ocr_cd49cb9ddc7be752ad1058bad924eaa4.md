The And/Or operators are the most common operators when working with complex criteria. The operators consider two different expressions (one on each side of the And/Or operators) and then determine whether the expressions are true or false. Then the operators compare the results of the two expressions against each other for a logical true/false answer. For example, take the first And statement in the expression given in the preceding paragraph:

```
(tblCustomers.State = "CA" AND tblProducts.Category <> "Cars")
```

The right side of the criteria (tblProducts.Category <> "Cars") evaluates to True if the Category is anything other than Cars. The And operator compares the logical true/false from the left and right expressions to return a true/false answer.

> NOTE
> A field has a null value when it has no value at all. Null indicates the lack of entry of information in a field. Null is neither true nor false, nor is it the same as a space character or 0. Null simply has no value. If you never enter a name in the City field and just skip it, Access leaves the field empty (unless a default value is provided in the table's design). This state of emptiness is known as null.

When the result of an And/Or operation is True, the overall condition is true, and the query displays the records meeting the true condition.

Notice that the result of an And operation is true only when both sides of the expression are true, whereas the result of an Or operation is true when either side of the expression is true. In fact, one side can be a null value, and the result of the Or operation will still be true if the other side is true. This is the fundamental difference between And/Or operators.

# Using functions in select queries

When you work with queries, you might want to use built-in Access functions to display information. For example, you might want to display items such as:

+   - The day of the week for sales dates
+   - All customer names in uppercase
+   - The difference between two date fields

You can display all this information by creating calculated fields for the query.

We discuss calculated fields in depth in Chapter 12 (and throughout this book).