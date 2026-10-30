# Figure 13.18

The VB three-axis model for referring to elements in a XML document.

![](bbox=[0.05, 0.14, 0.62, 0.42])

# The XML literals that you can use to refer to XML elements.

# Table 13.3

| XML element | XML literal | Example within a query |
|---|---|---|
| Child element | <element name> | ABook.<book> |
| Attribute | @attribute name | ABook.@ISBN |
| Descendant | ...<descendant name> | ABook...<price> |

The code to fill a list box in alphabetic order is

```
Retrieve the book data.
Dim BookQuery =
From ABook In BookData.<book>
Order By ABook...<title>.Value
Select ABook...<title>.Value
TitlesListBox.DataSource = BookQuery.ToList()
```

You can use the results as you would any other data. You also can do a further query on the result of the first query. Use a Where clause to "query the query" to find information about the book selected from the list box.

```
Dim SelectedBookQuery =
From SelectedBook In BookQuery
Where (SelectedBook...<title>.Value.ToString =
TitlesListBox.SelectedItem.ToString)
Select SelectedBook.<author>.Value,
SelectedBook.@ISBN, SelectedBook...<price>.Value
```