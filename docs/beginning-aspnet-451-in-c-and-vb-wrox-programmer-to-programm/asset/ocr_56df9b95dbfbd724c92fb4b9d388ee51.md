# Types of Controls

```
if (item.Selected == true)
{
  Labell.Text += "In the CBL you selected " + item.Value + "<br />";
}
```

Notice how in the VB.NET code the underscore is needed to split the code over two lines. VB.NET requires the underscore if you move the Handles key to

+   10. Save to the page and request it in the browser. Choose an item from the DropDownList, check or one items in the CheckBoxList, and click the button. You see seeing similar to Figure 4-8, which shows the page in Firefox.

![](bbox=[0.523, 0.191, 0.93, 0.383])

FIGURE 4-8

# How it Works

The various list controls all use <asp:ListItem> elements. It makes it easy to create them by copying from one to another. The DropDownList supports only one item at a time, it's pretty easy to get its value. All takes is a single line of code in C#):

```
Labell.Text = "In the CBL you selected " + DropList1.SelectedValue + "<br />";
```

The CheckBox control allows a user to select multiple items at once. Therefore, you need a bit more code to loop over the collection of items, checking the Selected property of each item (again shown in C#):

```
foreach (ListItem item in CheckBoxList1.Items)
{
  if (item.Selected == true)
  {
    Labell.Text += "In the CBL you selected " + item.Value + "<br />";
  }
}
```

The CheckList and the other list controls have Items that contains all the items you defined in the code. So, the code for Try It Out, CheckBoxList contains three items, for C#, Visual Basic, and CSS. Each ListItem in turn contains a property that determines or not the user has checked the item in list

Using a foreach loop (For Each VB.NET), you can iterate over collection of ListItems elements, testing the Selected property one by one. If the item was selected, its Selected property is true (True in VB) and its Value is appended to the text of the Label. Notice the use of += (&= in VB.NET) in the last example to assign the Value of the item together with the text to the Label's Text property. The += and &= syntax is shorthand for this:

Labell.Text = Labell.Text + "In the CBL you selected " + item.Value + "<br />";