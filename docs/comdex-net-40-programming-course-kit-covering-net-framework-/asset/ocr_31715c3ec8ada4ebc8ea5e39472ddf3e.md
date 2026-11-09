+   9. *Double-click* the Form1 to create the event handler for its Load event and add the highlighted code, given in Listing 6.9, to the Code Editor:

# Listing 6.9: Showing the Code for the Load Event of the Form

```
```csharp
private void Form1_Load(object sender, EventArgs e)
{
    string[] words = { "red", "blue", "white", "yellow", "green" };
    foreach (string w in words)
    {
        ListBox1.Items.Add(w);
    }
}
```
```

In the preceding code, we have declared an array of string type, words, and initialized the array with a set of string values. We have also added the elements of the array to the Items collection of the ListBox1 control on the form, by using a foreach loop.

+   10. *Double-click* the **Project Data** button in the form to create the event handler for its Click event and add the highlighted code, given in Listing 6.10, to the Code Editor:

# Listing 6.10: Showing the Code for the Click Event of the Project Data(button1) Button

```
```csharp
private void button1_Click(object sender, EventArgs e)
{
    string[] words = new string[5];
    for (int index = 0; index < 5; index++)
    {
        words[index] = listBox1.Items[index].ToString();
    }
    var query = from w in words select w.Substring(0, 1);
    foreach (string letter in query)
    {
        ListBox2.Items.Add(letter);
    }
}
```
```

In the preceding code, we have first declared an array of string type, words, and initialized the array with the items in the **ListBox1** control. After that, we have used the select clause in a LINQ query to select the first letter of all the elements of the array. Finally, we have added the set of letters to the Items collection of the **ListBox2** control.

+   11. Press the F5 key on the keyboard to run the application. The output of the application appears displaying a list of words in the first list box present on the form (Fig.C#-6.15).

+   12. Click the **Project Data** button (Fig.C#-6.15). The first letters, from the list of words in the first list box, are displayed in the second list box, as shown in Fig.C#-6.16:

![](bbox=[0.284, 0.661, 0.498, 0.825])

![](bbox=[0.526, 0.661, 0.739, 0.825])

After learning about projection operators, let’s now learn about the partitioning operators.