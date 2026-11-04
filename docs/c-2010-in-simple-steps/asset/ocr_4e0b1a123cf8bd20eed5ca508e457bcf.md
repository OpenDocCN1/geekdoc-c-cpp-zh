![](bbox=[0.22, 0.14, 0.74, 0.35])

Fig.C# -6.25

The selected controls are added to the statusStrip1 control (Fig.C# -6.26).

16 Double-click the textBox1 control, as shown in Fig.C# -6.26:

![](bbox=[0.33, 0.42, 0.62, 0.6])

Fig.C# -6.26

17 Add the highlighted code, given in Listing 6.5, in the TextChanged event of textBox1:

# Listing 6.5: Showing the Code of textBox1_TextChanged Event

```
private void textBox1_TextChanged(object sender, EventArgs e)
{
    string[] str = textBox1.Text.Split(new char[] {'\n'});
    toolStripStatusLabel1.Text = ("Words: " + str.Length + ", " + "Characters " + textBox1.TextLength);
}
```

18 Press the F7 key to switch to the designer and double-click the statusStrip1 control. Add the highlighted code, given in Listing 6.6, in the ItemClicked event of the statusStrip1 control:

# Listing 6.6: Showing the Code of statusStrip1_ItemClicked Event

```
private void statusStrip1_ItemClicked(object sender, ToolStripItemClickedEventArgs e)
{
    MessageBox.Show("Item clicked: " + e.ClickedItem.Name);
}
```