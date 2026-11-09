# Listing 6.7: Showing the Code for the Load Event of the Form

```
```csharp
private void Form1_Load(object sender, EventArgs e)
{
    int[] doubles = { 1, 2, 3, 4, 5, 6, 7, 8, 9};
    foreach (int i in doubles)
    {
        ListBox1.Items.Add(i.ToString());
    }
}
```
```

In the preceding code, we have first declared an array of integer type, doubles, and initialized the array with a set of integer values. We have also added the elements of the array to the Items collection of the ListBox1 control on the form, by using a foreach loop.

+   10. Double-click the Filter Data button in the form to create the event handler for its Click event and add the highlighted code, given in Listing 6.8, to the Code Editor:

# Listing 6.8: Showing the Code for the Click Event of the Filter Data (button1) Button

```
```csharp
private void button1_Click(object sender, EventArgs e)
{
    int[] doubles = new int [9];
    for (int i = 0; i < 9; i++)
    {
        doubles[i] = Convert.ToInt32(listBox1.Items[i]);
    }
    var numQuery = from num in doubles where (num % 2) == 0 select num;
    listBox2.Items.Clear();
    foreach (int num in numQuery)
    {
        listBox2.Items.Add(num.ToString());
    }
}
```
```

In the preceding code, we have first declared an array of integer type, doubles, and initialized the array with the items in the ListBox1 control. After that, we have used the where clause in a LINQ query, numQuery, to retrieve even values from the array. Finally, we have added the filtered values to the Items collection of the ListBox2 control.

+   11. Press the F5 key on the keyboard to run the application. The output of the application appears displaying a list of values in the first list box present on the form (Fig.C#-6.12).
+   
+   12. Click the Filter Data button (Fig.C#-6.12). The even values, from the list of values in the first list box, are displayed in the second list box, as shown in Fig.C#-6.13:

![](bbox=[0.294, 0.673, 0.509, 0.84])

![](bbox=[0.533, 0.673, 0.747, 0.84])

Fig.C#-6.12

Fig.C#-6.13