# CREATE SOME WINDOW ELEMENTS

Next up, we'll add some elements to our window so that we can exercise our event handler. Add a Button, TextBox, ListBox and some RadioButtons (inside a GroupBox). Here's my version:

```
<Window ... Loaded="ShowArguments">
<Grid>
<Button Content="Click Me" Name="button1" ... />
<TextBox Name="textBox1" ... >I'm some text</TextBox>
<ListBox Name="listBox1" ...>
<ListBoxItem>Pick Me!</ListBoxItem>
<ListBoxItem>No, Pick Me!</ListBoxItem>
</ListBox>
<GroupBox Header="Radio Group" Name="groupBox1" ...>
<StackPanel>
<RadioButton>First Item</RadioButton>
<RadioButton>Second Item</RadioButton>
<RadioButton>Third Item</RadioButton>
</StackPanel>
</GroupBox>
</Grid>
</Window>
```

Make sure to set the Width of the the Listbox so that it's bigger than the two items. (You'll see why in a few pages...)

![](bbox=[0.095, 0.665, 0.495, 0.905])