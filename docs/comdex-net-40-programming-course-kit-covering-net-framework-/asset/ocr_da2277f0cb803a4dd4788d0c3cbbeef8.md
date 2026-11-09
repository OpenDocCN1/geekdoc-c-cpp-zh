![](bbox=[0.338, 0.139, 0.686, 0.339])

Fig.VB-7.1

+   8. Double-click the Create List button in the form to create the event handler for its Click event and add the highlighted code snippet shown in Listing 7.1 to Code Editor:

Listing 7.1: Showing the Use of a LINQ Query

```
```vb
Private Sub Button1_Click(ByVal sender As System.Object, ByVal e As
    System.EventArgs) Handles Button1.Click
    Dim numbers As Integer() = New Integer(6) {0, 1, 2, 3, 4, 5, 6}
    Dim numQuery = From num In numbers Where (num Mod 2) = 0 Select num
    For Each num As Integer In numQuery
        ListBox1.Items.Add(num.ToString())
    Next num
End Sub
```
```

The highlighted code snippet in Listing 7.1 shows how to create and use a simple LINQ query. Listing 7.1 uses an integer array, numbers, as the data source for the LINQ query. Then, we create the numQuery query that selects even numbers from the numbers array. Finally, the query is executed within the For Each statement, where the query result set is added to a list box.

+   9. Press the F5 key to run the application. The output of the application appears (Fig.VB-7.2).

+   10. Click the Create List button (Fig.VB-7.2). A list of even numbers is created and added to the list box, as shown in Fig.VB-7.3.

![](bbox=[0.308, 0.64, 0.48, 0.715])

![](bbox=[0.531, 0.64, 0.714, 0.715])

Fig.VB-7.2

Fig.VB-7.3

This was just a simple example of creating a LINQ query. Let’s now learn about the standard query operators used in LINQ.

# # Working with Standard Query Operators

The standard query operators are the methods that form the LINQ pattern. These operators provide querying capabilities, including filtering, projection, aggregation, and sorting. The standard query