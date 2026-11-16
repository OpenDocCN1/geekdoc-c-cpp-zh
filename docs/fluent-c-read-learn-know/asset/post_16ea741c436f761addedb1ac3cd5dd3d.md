
## 1 BUILD THE UI

We'll start by building the basic window that contains a DockPanel, a TreeView containing several items at two levels, and a TabControl with one TabItem. If you'd like to use something other than Recipes in your sample, feel free (you could go back to that list of applications you want to write), but for our purposes, you'll want a two-level hierarchy with details to be displayed in tabs.

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_589_0.png)

The TreeView is docked to the left.

Setting LastChildFill to true takes care of the size and position of the TabControl.

This is just a Label inside the TabItem that tells the user what they need to do to display the recipe details.

## PUT ON YOUR THINKING HAT

Create a new Visual Studio WPF project and build the basic window as shown.

## HOW'D YOU DO?

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_590_0.png)

Here's the basic structure of my version of the XAML. Your fonts and sizes will be different, and if you used a different hierarchy, that's just fine.

```
<DockPanel LastChildFill="True">
<TreeView Name="RecipeList" DockPanel.Dock="Left" Width="250"
FontSize="18" MouseDoubleClick="TreeView_MouseDoubleClick">
<TreeViewItem Header="Appetizers">
<TreeViewItem Header="Mini Crostini" />
<TreeViewItem Header="Mixed Tarts" />
<TreeViewItem Header="Mezze Platter" />
<TreeViewItem Header="Classic Sliders" />
<TreeViewItem Header="Buffalo Wings" />
<TreeViewItem>
<TreeViewItem Header="Main Courses">
...
<TreeViewItem>
<TreeViewItem Header="Desserts">
...
<TreeViewItem>
</TreeView>
<TabControl Margin="10,10" Name="RecipeTab">
<TabItem>
<TabItem.Header>
Remember the name, it's
important
<StackPanel>
<Label FontSize="12" HorizontalAlignment="Center"
Height="25">No category</Label>
<Label FontSize="18" HorizontalAlignment="Center"
Height="35">Blank</Label>
</StackPanel>
</TabItem.Header>
<TabItem.Header>
<Label>Select an item to display it</Label>
</TabItem>
</TabControl>
</DockPanel>
```

It's important to name the elements that we'll refer to in code, but it's fine if you choose different names as long as they make sense to you.

The name of this method will be different, depending on when you created the handler. I created nine before I set the element name.

You'll have the second-level items here. I didn't have room, so I've left them out of the sample.

## PUT ON YOUR THINKING HAT

We only have a single method to write: the MouseDoubleClick event handler. But before we jump into coding, let's spend some time thinking about what needs to be done, and in what order. In the list below, three of the action items are unnecessary. Can you spot the ones that you won't need, and put the rest in order?

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_591_0.png)

- Get a reference to the item that was double-clicked.
- Add two labels to the header StackPanel.
- Add the new tab to the TabControl.
- Create a new TabItem.
- Select the new tab.
- Create a StackPanel for the header.
- Create a Label containing the recipe name.
- Create a TabControl.
- Set the Header property of the TabItem to a StackPanel
- Check that the selected item is in the second level of the hierarchy
- Get a reference to the parent of the item that was double-clicked.
- Select an item in the TreeView.
- Set the FontFamily and FontSize of the Window.
- Create a Label containing the recipe category name.

## HOW'D YOU DO?

Here's the order I'd do the items, but notice that not all of them need to be done in a particular order. For example, while you have to add the two labels to the StackPanel in a particular order to get them to display correctly, you can create the labels in any order.

- 1 Get a reference to the item that was double-clicked.
- 8 Add two labels to the header StackPanel.
- 10 Add the new tab to the TabControl.
- 4 Create a new TabItem.
- 11 Select the new tab.
- 5 Create a StackPanel for the header.
- 7 Create a Label containing the recipe name.
- x Create a TabControl.
- 9 Set the Header property of the TabItem to a StackPanel.
- 2 Check that the selected item is in the second level of the hierarchy.
- 3 Get a reference to the parent of the item that was double-clicked.
- x Select an item in the TreeView.
- x Set the FontFamily and FontSize of the Window.
- 6 Create a Label containing the recipe category name.

## PUT ON YOUR THINKING HAT

Okay, it's time to write the code. The list of action items is below, with some notes to get you started. You might also want to check back to that first exercise to remind yourself of the methods and properties you'll need to use.

- 1. Get a reference to the item that was double-clicked.
  Remember, you'll have to cast the SelectedItem property to a TreeViewItem.

- 2. Check that the selected item is in the second level of the hierarchy.
  If it isn't, you can just return.

- 3. Get a reference to the parent of the item that was double-clicked.

- 4. Create a new TabItem.

- 5. Create a StackPanel for the header.

- 6. Create a Label containing the recipe category name.
  Remember to set the FontSize and Height properties. Check the XAML for the values.

- 7. Create a Label containing the recipe name.

- 8. Add two labels to the header StackPanel.
  Remember to add them in the right order, recipe name first.

- 9. Set the Header property of the TabItem to a StackPanel.

- 10. Add the new tab to the TabControl.

- 11. Select the new tab.

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_594_0.png)

## HOW'D YOU DO?

Here's my version. As long as yours works, don't worry if your code's a little different...

```
private void TreeView_MouseDoubleClick(object sender, MouseButtonEventArgs e)
{
    //get a reference to the item the user double-clicked
    TreeViewItem tv = (TreeViewItem) RecipeList.SelectedItem;

    //if the parent of this item isn't a TreeViewItem, it's a first-level object,
    //so we don't want to do anything.
    if (tv.Parent.GetType().Name == "TreeView")
        return;

    //get a reference to the parent
    TreeViewItem parentTv = (TreeViewItem)tv.Parent;

    //create the new Tab
    TabItem NewTab = new TabItem();

    //create the header
    StackPanel RecipeHeader = new StackPanel();

    //Create the category label
    Label Category = new Label();
    Category.Content = parentTv.Header;
    Category.FontSize = 12;
    Category.Height = 25;
    Category.HorizontalContentAlignment = System.Windows.HorizontalAlignment.Center;

//Create the recipe name label
Label RecipeName = new Label();
RecipeName.Content = tv.Header;
RecipeName.FontSize = 18;
RecipeName.Height = 35;
RecipeName.HorizontalContentAlignment = System.Windows.HorizontalAlignment.Center;

//Add the labels to the header StackPanel
RecipeHeader.Children.Add(Category);
RecipeHeader.Children.Add(RecipeName);

//Add the header to the new tab
NewTab.Header = RecipeHeader;

//Add the tab to the TabControl and select it
RecipeTab.Items.Add(NewTab);
NewTab.IsSelected = true;
}
```

## TAKE A BREAK

That wasn’t just an exercise you just did; that was REAL programming, as in “people get paid to do this.” I sure hope you enjoyed it! Why don’t you take a break now, before we finish up the chapter?

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_595_0.png)

## REVIEW

You've worked really hard in this chapter, but this should be pretty easy. Can you put each of the classes in the list into their place in the class hierarchy?

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_596_0.png)

- FrameworkElement
- Control
- Calendar
- ContentControl
- Window
- Button
- TabItem
- Label
- ItemsControl
- TreeView
- TabControl
- Panel
- DockPanel
- Grid
- StackPanel
- Selector
- ListBox
- ComboBox

## Congratulations! You've finished the chapter. Take a minute to think about what you've accomplished before you move on to the next one...

List three things you learned in this chapter:

- 1
- 2
- 3

Why do you think you need to know these things in order to be a C# programmer?

Is there anything in this chapter that you think you need to understand in more detail? If so, what are you going to do about that?
