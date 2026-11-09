From this we can see that, in HTML, the recipe for a table is:

+   1. Add one or more table row elements.
+   2. Fill each row with table header or table data elements.

The HTML elements are named as shown to the right.

table row — `tr`
table header — `th`
table data — `td`

If we use the element names, our diagram looks like this:

| th | th | th | th |
|---|---|---|---|
| td | td | td | td |
| td | td | td | td |
| td | td | td | td |
| td | td | td | td |
| td | td | td | td |

From this we can see what the actual HTML markup should look like if the table was empty:

```
<h2>Upcoming Concerts</h2>
<table>
<tr>
<th></th><th></th><th></th><th></th>
</tr>
<tr>
<td></td><td></td><td></td><td></td>
</tr>
<tr>
<td></td><td></td><td></td><td></td>
</tr>
<tr>
<td></td><td></td><td></td><td></td>
</tr>
<tr>
<td></td><td></td><td></td><td></td>
</tr>
<tr>
<td></td><td></td><td></td><td></td>
</tr>
</table>
```

> We call this the **table skeleton** because this just the bones of the table. We haven't added the actual content yet.

![](bbox=[0.686, 0.468, 0.915, 0.733])

# NINJA TIP

![](bbox=[0.039, 0.785, 0.101, 0.844])

If you're creating a table, it's best to begin by working out how many rows and columns your table will have and then creating the skeleton, otherwise tables can get pretty confusing. Make sure when you create the skeleton that all the opening and closing tags are in the correct place. Notice how there are four `th` elements in the first row and then four `td` elements in the following rows. These tags are surrounded by `tr` opening and closing tags.