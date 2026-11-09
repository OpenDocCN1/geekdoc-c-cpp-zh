![](bbox=[0.309, 0.141, 0.714, 0.371])

Fig.VB-7.11

9. *Double-click* the form to create the event handler for its **Load** event and add the highlighted code snippet shown in Listing 7.7 to Code Editor:

# **Listing 7.7:** Handling the Load Event of the Form

```
Private Sub Form1_Load(ByVal sender As System.Object, ByVal e As System.EventArgs)
    Handles MyBase.Load
    Dim values() As Integer = {1, 2, 3, 4, 5, 6, 7, 8, 9}
    For Each v In values
        ListBox1.Items.Add(v.ToString())
    Next
End Sub
```

Listing 7.7 shows the code for the event handler of the Load event of Form1. In the highlighted code snippet, we first declare an array of Integer type, values, and initialize the array with a set of integer values. Then, we add the elements of the values array to the Items collection of the first ListBox1 control on the form, by using the For Each loop.

10. *Double-click* the Filter Data button in the form to create the event handler for its **Click** event and add the highlighted code snippet shown in Listing 7.8 to Code Editor:

# **Listing 7.8:** Handling the Click Event of the Button1

```
Private Sub Button1_Click(ByVal sender As System.Object, ByVal e As
    System.EventArgs) Handles Button1.Click
    Dim values(8) As Integer
    For index = 0 To 8
        values(index) = ListBox1.Items(index)
    Next
    Dim filteredValues = From v In values Where v Mod 2 = 0 Select v
    ListBox2.Items.Clear()
    For Each v In filteredValues
        ListBox2.Items.Add(v.ToString())
    Next
End Sub
```

Listing 7.8 shows the code for the event handler of the Click event of Button1. In the highlighted code snippet, we first declare an array of Integer type, values, and initialize the array with the items in the ListBox1 control. Then, we use the Where clause in the filteredValues query, to retrieve even values from the array. Finally, we add the filtered values to the Items collection of the ListBox2 control.

11. *Press* the F5 key to run the application. The output of the application appears, displaying a list of values in the first list box present on the form (Fig. VB-7.12).