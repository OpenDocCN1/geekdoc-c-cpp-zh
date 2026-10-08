# 662 Chapter 15 Graphical User Interfaces with Windows Forms: Part 2

```
5
6 namespace CheckedListBoxTest
7 {
8     // Form uses a Checked List to add items to a display ListBox
9     public partial class CheckedListBoxForm : Form
10    {
11        // constructor
12        public CheckedListBoxForm()
13        {
14             InitializeComponent();
15        }
16 
17        // item checked or unchecked
18        // add or remove from display ListBox
19         private void itemCheckedListBoxCheck(
20             object sender, ItemCheckArgs e)
21         {
22             // reference of selected item
23             string item = itemCheckedListBox.SelectedItem.ToString();
24 
25             // if item checked, add to ListBox
26             // otherwise remove from ListBox
27             if (e.NewValue == CheckState.Checked)
28             {
29                 ListBox.Items.Add(item);
30             }
31             else
32             {
33                 ListBox.Items.Remove(item);
34             }
35         }
36 }
```

a) Initial GUI displayed when the app executes

b) GUI after selecting the first three items

c) GUI after deselecting C++ HTP

d) GUI after selecting C# HTP

![](bbox=[0.116, 0.621, 0.856, 0.843])

When the user checks or unchecks an item in itemCheckedListBox, an ItemCheck event occurs and event handler itemCheckedListBoxCheck (lines 19–35) executes. An if...else statement (lines 27–34) determines whether the user checked or unchecked