+   9. Double-click the form to create the event handler for its Load event and add the highlighted code, given in Listing 6.5, to the Code Editor:

Listing 6.5: Showing the Code for the Load Event of the Form

```
private void Form1_Load(object sender, EventArgs e)
{
    int[] doubles = { 1, 2, 2, 3, 4, 5, 5 };
    foreach (int i in doubles)
    {
        listBox1.Items.Add(i.ToString());
    }
}
```

In the preceding code, we have first declared an array of integer type, doubles, and initialized the array with a set of integer values. We have also added the elements of the array to the Items collection of the ListBox1 control on the form, by using a foreach loop.

+   10. Double-click the Show Distinct Values button in the form to create the event handler for its Click event and add the highlighted code, given in Listing 6.6, to the Code Editor:

Listing 6.6: Showing the Code for the Click Event of the Show Distinct Values(button1) Button

```
private void button1_Click(object sender, EventArgs e)
{
    int[] val = new int[7];
    for (int index = 0; index < 7; index++)
    {
        val[index] = Convert.ToInt32(listBox1.Items[index]);
    }

    var dist = (from v in val select v).Distinct();
    listBox2.Items.Clear();
    foreach (int v in dist)
    {
        listBox2.Items.Add(v);
    }
}
```

In the preceding code, we have first declared an array of integer type, val, and initialized it by the ListBox1 items. After that, we have used the Distinct clause in a LINQ query, dist, to remove duplicate values from the array. Finally, we have added the distinct values to the Items collection of the ListBox2 control.

+   11. Press the F5 key on the keyboard to run the application. The output of the application appears displaying a list of values with some duplicate values in the first list box (Fig.C#-6.9).

+   12. Click the Show DistinctValues button (Fig.C#-6.9). The distinct values, from the list of values in the firstlistbox, are displayed in the second listbox, as shown in Fig.C#-6.10:

![](bbox=[0.286, 0.661, 0.477, 0.799])

![](bbox=[0.529, 0.661, 0.738, 0.799])

Fig.C#-6.9

Fig.C#-6.10

In this way, by using the Distinct clause, you can find unique elements from a given sequence.