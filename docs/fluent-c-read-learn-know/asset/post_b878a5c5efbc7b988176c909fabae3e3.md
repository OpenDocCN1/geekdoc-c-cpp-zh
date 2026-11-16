
## THE TREEVIEW

The TreeView, which displays hierarchical data, is the only common control that descends directly from ItemsControl. (Most descend by way of the Selector class.) Like many of the items controls, the TreeView re-defines the Items collection to be a collection of a specific type, in this case TreeViewItem, which is itself an items control, by way of HeaderedItemsControl.

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_580_0.png)

The TreeViewItem is itself an items control, which allows it to contain a collection of children.

### PUT ON YOUR THINKING HAT

Using XAML collection syntax, can you work out how to specify the collections that create the TreeView shown? (If you've forgotten how collection syntax works, check page 513. Hint: You specify the text shown by the TreeView using the Header property.

```
MainWindow
First Top Level Item
  I'm a child
  I'm a child, too
Second Top Level Item
  One
  Two
  Three
  Four
Last Item
  A
  B
    B1
    B2
  C
```

## HOW'D YOU DO?

Was it a poser, or did you find it easy to figure out? Don't give up if it was a bit difficult. I promise it will get easier with practice.

Did I catch you? Collection syntax is how you specify the content of a panel, too.

```
<TreeView FontFamily="Brandywine"
FontSize="24">
<TreeViewItem Header="First Top Level Item">
<TreeViewItem Header="I'm a child" />
<TreeViewItem Header="I'm a child, too" />
</TreeViewItem>
<TreeViewItem>
<TreeViewItem Header="Second Top Level Item">
<TreeViewItem Header="One" />
<TreeViewItem Header="Two" />
<TreeViewItem Header="Three" />
<TreeViewItem Header="Four" />
</TreeViewItem>
<TreeViewItem Header="Last Item">
<TreeViewItem Header="A" />
<TreeViewItem Header="B" />
<TreeViewItem Header="B1" />
<TreeViewItem Header="B2" />
<TreeViewItem Header="C" />
</TreeViewItem>
</TreeView>
```

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_582_1.png)

The TreeViewItem collection can be nested as deeply as you need them to be.

## THE LISTBOX AND COMBOBOX

The ListBox and ComboBox controls are two of the most commonly used items controls. They both descend from the Selector class, which adds properties that allow the user to select items in the control.

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_583_0.png)

We'll talk about the difference between SelectedItem (the actual item the user chose) and SelectedValue (the value of a specified property associated with the SelectedItem) when we look at WPF binding in Chapter 22.

Because ListBoxItem descends from ContentControl, not ItemsControl, you set the Content property, not the Header.

The ListBox and ComboBox also define distinct types for their item collection. As you can see, ComboBoxItem inherits from ListBoxItem.

### PUT ON YOUR THINKING HAT

We've been working in XAML a lot in this chapter, so let's do something in C#. Can you write an application that displays a ListBox with three or four items, selects the second item in the list when the Window is loaded, and then displays the SelectedIndex in a MessageBox when the user chooses something else? (Hint: You'll need to add an event handler. Do you remember how to do that from the Properties window?) When you run the application, it will display the MessageBox twice. Do you know why?

## HOW'D YOU DO?

The application displays the MessageBox first when you set the SelectedIndex in code. We'll find out how to fix that in the next chapter.

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_584_0.png)

## THE XAML

There's nothing too tricky here, as long as you didn't follow the TreeView sample too closely—ListBoxItem is a content control, so you can either set the Content property explicitly using attribute syntax, or implicitly using content syntax, as I've done here.

```
<Grid>
    <ListBox Name="SampleListBox" Margin="10,10">
        <ListBoxItem>First Item</ListBoxItem>
        <ListBoxItem>Second Item</ListBoxItem>
        <ListBoxItem>Third Item</ListBoxItem>
        <ListBoxItem>Fourth Item</ListBoxItem>
    </ListBox>
</Grid>
```

## SELECT THE SECOND ITEM

The best place to do this is in the window constructor, which should look like this:

```
public MainWindow()
{
    InitializeComponent();
    this.SampleListBox.SelectedIndex = 1;
}
```

Did you remember to count from zero?

## RESPOND TO A SELECTIONCHANGED EVENT

This one is easy if you do it from the Properties window. Otherwise, the syntax for the method is tedious:

```
private void SampleListBox_SelectionChanged(object sender, SelectionChangedEventArgs e)
{
    MessageBox.Show(this.SampleListBox.SelectedIndex.ToString());
}
```

## TAB CONTROLS

Before we finish up the chapter with an exercise that combines all we've learned, let's take a quick look at the TabControl, which is another useful mechanism for managing your screen real estate. Modern applications have largely replaced the older MDI structure that uses child windows with tabbed windows. The only new property you need to deal with is TabStripPlacement. You already know everything else you need to use this control. Are you impressed? I am!

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_585_0.png)

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_585_1.png)

The TabStripPlacement property in TabItem is read-only.

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_585_2.png)

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_585_3.png)

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_585_4.png)

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_585_5.png)

The TabStripPlacement property lets you control where the tab label appear.

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_585_6.png)

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_585_7.png)

### PUTTING IT ALL TOGETHER

We'll finish up this chapter with an extended exercise that uses what we've learned to rough out a real application component. Here's what it's going to look like:

When it first opens, the application will display a list of recipes in a TreeView, and a TabControl with a single blank tab.

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_586_0.png)

When the user double-clicks a recipe in the TreeView, we'll open up a new tab. (We won't worry about the contents of the tab right now, just the header.)

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_586_1.png)

### PUT ON YOUR THINKING HAT

Before we jump in coding, take some time to think about what we need to do. Can you answer these questions?

The main window has a TreeView on the left and a TabControl on the right. When the window is re-sized, the width of the TreeView remains the same. What panel type do you think will be best to use as the layout root?

The TabItem has two items in its Header. How will you do that? (Hint: the Header property is defined as an Object.)

When an item in the list of recipes is double-clicked, a new tab will open. You'll need to put that code in an event handler. What event do you think you should respond to? (Hint: Check the available events in the Properties window when the TreeView is selected.)

What property can you use to get a reference to the item the user double-clicked?

The tab header lists both the recipe name and the type of recipe (e.g., “Appetizers” or “Desserts”. What property can you use to get a reference to the type of recipe?

Our recipe hierarchy has two levels. You'll only want to add a new tab if the user double-clicks a second level item (e.g., “Mini Crostini”, not “Appetizers”). How do you think you can check that? (Hint: Remember the GetType() method?)

To add the new TabItem, you'll need to create it, and then add it to the TabControl's item collection. How do you think you'll do that?

It will be convenient for the tab you've just added to be selected in the TabControl once you add it. That doesn't happen automatically. What property of the TabItem will you set to select it?

### HOW'D YOU DO?

Here's the way I'm going to approach the problem. But remember, there are very few absolutes in programming. If you answered these questions differently, can you justify your answers?

- **What panel type do you think will be best to use as the layout root?**
  *I'm going to use a DockPanel, but other panels would work, too.*

- **The TabItem has two items in its Header. How will you do that?**
  *There are other ways, but the easiest is probably to put the two labels in a panel. I'm going to use a StackPanel.*

- **What event do you think you should respond to?**
  *We'll use the MouseDoubleClick event.*

- **What property can you use to get a reference to the item the user double-clicked?**
  *We can use SelectedItem.*

- **What property can you use to get a reference to the type of recipe?**
  *The Parent property of the selected property will give us the reference, but we'll have to cast both objects to TreeViewItem.*

- **You'll only want to add a new tab if the user double-clicks a second level item. How do you think you can check that?**
  *You can test for Parent.GetType().Name == "TreeView"*

- **To add the new TabItem, you'll need to create it, and then add it to the TabControl's item collection. How do you think you'll do that?**
  *We can call the Add() method of the Items collection.*

- **What property of the TabItem will you set to select it?**
  *We just need to set IsSelected to true.*
