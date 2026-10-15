```
{
    ListViewItem lItem = listView1.Items.Add(obj.ToString());
    lItem.SubItems.Add(DictStr[(int)obj]);
}
}
private void button2_Click(object sender, EventArgs e)
{
string tempKey = Microsoft.VisualBasic.Interaction.InputBox("Enter the key to look up", "", "", -1, -1);
if (DictStr.ContainsKey(Convert.ToInt32(tempKey)))
{
    MessageBox.Show("The dictionary contains the specified key");
}
else
{
    MessageBox.Show("The dictionary does not contain the specified key");
}
private void button3_Click(object sender, EventArgs e)
{
string tempKey = Microsoft.VisualBasic.Interaction.InputBox("Enter the value to look up", "", "", -1, -1);
if (DictStr.ContainsValue(tempKey))
{
    MessageBox.Show("The dictionary contains the specified value");
}
else
{
    MessageBox.Show("The dictionary does not contain the specified value");
}
}
}
```

In Listing 32.10, we have created an object, DictStr, of the Dictionary<TKey, TValue> class. Next, in the Click event of button1, we have used the Add method to add elements in the DictStr object. Then, in the Click events of button2 and button3, we have used the ContainsKey and ContainsValue methods to search an element key or value in the Dictionary<TKey, TValue> object, respectively.

+   7. Press the F5 key to execute the application. When the form appears, click the Create and add 10 items button. The Dictionary<TKey, TValue> object is created and 10 elements are stored in it, and the ListView control is populated with these elements, as shown in Figure 32.38:

![](bbox=[0.35, 0.665, 0.72, 0.9])

Figure 32.38: Adding Elements to the Dictionary<TKey, TValue> Object