**Listing 7.13: Handling the Click Event of the Button2**

```
```vb
Private Sub Button2_Click(ByVal sender As System.Object, ByVal e As
    System.EventArgs) Handles Button1.Click
    Dim numbers(9) As Integer
    For index = 0 To 9
        numbers(index) = ListBox1.Items(index)
    Next
    Dim query = From p In numbers Skip 4
    ListBox2.Items.Clear()
    For Each p In query
        ListBox2.Items.Add(p.ToString())
    Next
End Sub
```
```

Listing 7.13 shows the code for the event handler of the Click event of Button2. In the highlighted code snippet, we first declare an array of the Integer type, numbers, and initialize the array with the items in the ListBox1 control. Then, we use the Skip clause in a LINQ query to retrieve all except the first four elements from the numbers array. Finally, we add the retrieved values to the Items collection of the ListBox2 control.

+   13. **Press** the **F5** key to run the application. The output of the application appears, displaying a list of values in the first list box present on the form (Fig.VB-7.18).
+   14. **Click** the **Take 5** button (Fig.VB-7.18). The first five values, from the list of values in the first list box, are displayed in the second list box (Fig.VB-7.19).
+   15. **Click** the **Skip 4** button (Fig.VB-7.19). All except the first four elements from the first list box are displayed in the second list box, as shown in Fig.VB-7.20:

![](bbox=[0.187, 0.448, 0.386, 0.551])

![](bbox=[0.442, 0.448, 0.595, 0.551])

![](bbox=[0.65, 0.448, 0.803, 0.551])

You can notice in Fig.VB-7.19 and Fig.VB-7.20 that the partitioning operators divide a given sequence into two sequences, and return one of them, without rearranging the elements.

# ### Grouping Operators

Grouping operators in LINQ are used to put data into groups so that the elements in each group share a common attribute. For example, there is a set of fruit names and you want to divide all the fruit names in groups according to their first letter. In this situation, you can use the Grouping operator.

Table 7.7 lists all the grouping operators in LINQ:

**Table 7.7: Grouping Operators in LINQ**

| Operator | Description | Query Expression Syntax (Visual Basic) |
| --- | --- | --- |
| GroupBy | Groups the elements of a collection based on a shared attribute | Group ... By ... Into ... |
| ToLookup | Creates a lookup data structure, which contains key-value pairs, from a collection of objects | Not available |

Perform the following steps to group a set of words by using the **Group By** clause: