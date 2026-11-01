The CheckBoxList control enables a user to select multiple items at once. Therefore, you need a bit more code to loop over the collection of items, checking the Selected property of each item (again shown in C#):

```
```csharp
foreach (ListItem item in CheckBoxList1.Items)
{
    if (item.Selected == true)
    {
        Label1.Text += "In the CBL you selected " + item.Value + "<br />";
    }
}
```
```

The CheckBoxList and the other list controls have an Items collection that contains all the items you defined in the code. So, given the code from this Try It Out, CheckBoxList1 contains three items, for C#, Visual Basic, and CSS, respectively. Each ListItem in turn contains a Selected property that determines whether or not the user has checked the item in the list.

Using a foreach loop (For Each in VB.NET), you can iterate over the collection of ListItem elements, testing the Selected property one by one. If the item was selected in the list, its Selected property is true (True in VB) and its Value is appended to the text of the Label. Notice the use of += ( &= in VB.NET) in the last code example to assign the Value of the list item together with the text to the Label control's Text property. The += and &= syntax is shorthand for this:

```
```csharp
Label1.Text = Label1.Text + "In the CBL you selected" + item.Value + "<br />";
```
```

This code takes the current text from the Label control, appends the literal text "In the CBL you selected" to it, then appends the value of the item using item.Value and finally appends the literal text "<br />". It then reassigns the entire string back to the Text property of the label. Using the += syntax is often a bit easier to write and understand, but the longer version is common as well.

Both VB.NET and C# have support for a for each loop, although both languages use a slightly different syntax. In the next chapter, you learn a lot more about looping and other language constructs.

Also of note is the way the ListItems are set up. In the first example, before the Try It Out, you saw ListItem elements with both a value and text:

```
```html
<asp:ListItem Value="C#">C#</asp:ListItem>
<asp:ListItem Value="Visual Basic">Visual Basic</asp:ListItem>
<asp:ListItem Value="CSS">CSS</asp:ListItem>
```
```

When you add items to the list yourself with the ListItem Collection Editor, you don't get the Value attributes:

```
```html
<asp:ListItem>C#</asp:ListItem>
<asp:ListItem>Visual Basic</asp:ListItem>
<asp:ListItem>CSS</asp:ListItem>
```
```

You didn't get the Value attribute because you didn't supply an explicit value for the item in the ListItem Collection Editor. If you omit the Value, the text between the opening and closing tags of the ListItem is used implicitly as the value, which is fine in many cases. However, it's also quite common to have a different Value and Text property in the list. For example, when you have a list with countries, you could use the full name of the country as the Text (like The Netherlands) and use the official country code (nl) as the Value for the drop-down list. You see the list controls at work in other chapters in this book.