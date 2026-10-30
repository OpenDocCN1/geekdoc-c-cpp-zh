For the query, our In clause will address the name of the array, Amount Decimal. The In clause always refers to the name of the object, which could be an array or even an Items collection from a list box such as SchoolListBox. Items. The From is one element in the collection and does not need to be declared. Think of the From object as the same as a single element in a For each loop.

The query is called BelowMinimumQuery. Using type inference, your Dim statement becomes

```
Dim BelowMinimumQuery = _
    From AnItem In AmountDecimal _
    Where AnItem < 100D _
    Select AnItem
```

The Where clause allows us to provide a condition; if we want all records in a collection, just omit the Where clause. Notice that this Where checks to see if an item is less than one hundred. The Select clause then executes the query giving us a result set in BelowMinimumQuery. You may then use the query results as a new collection. In this example, we are going to display the items in a list box using the ToList method of the query object.

```
'Project       Ch13LinqArray
'Programmer    Bradley/Millspaugh
'Date          June 2009
'Description   Use LINQ to query an array.

Public Class LinqForm

    Private Sub Form1_Load(ByVal sender As System.Object, _
        ByVal e As System.EventArgs) Handles MyBase.Load
        'Display the amounts below the minimum of 100
        Dim AmountDecimal() As Decimal = {100D, 50D, 35.75D, 123.1D, 12.4D}

        Dim BelowMinimumQuery = _
            From AnItem In AmountDecimal _
            Where AnItem < 100D _
            Select AnItem

        BelowMinimumListBox.DataSource = BelowMinimumQuery.ToList()
    End Sub
End Class
```

# Additional LINQ Keywords

Many other operators are available for LINQ queries (see Table 13.2), including sorting and grouping. The aggregate operators include Average, Count, Max, Min, and Sum, giving you a lot of power for finding summary information from a table through a query.

# LINQ to SQL

You can apply a LINQ query to a relational database, even though the database’s language is not based on objects. To use LINQ with a database, you need to add a new item to a database project called the LINQ to SQL Classes template. In a project that already has a form and data source defined, select Project / Add New item and select LINQ TO SQL Classes from the Templates list.