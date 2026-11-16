
## HEADERED CONTENT CONTROLS

Another important branch of the content control class hierarchy are the controls that descend from HeaderedContentControl. Headered content controls are controls that have both a single item of content, and a single header. One of the cool things about headered content controls is that, like the content itself, the header can be any object, including, for example, an Image or a panel that itself contains multiple elements.

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_571_0.png)

Expander control can open to the left, right, top or bottom, depending on the setting of the ExpandDirection property.

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_571_1.png)

A GroupBox only contains its content in a box, but it's commonly used to control the behavior of a set of RadioButton controls. (We'll discuss those in the next section.)

The Expander control doesn't support scrolling directly. This content is wrapped in a ScrollViewer.

When an Expander is expanded, it pushes other content out of the way.

### PUT ON YOUR THINKING HAT

Can you re-create the example window? Here are some hints:

- The layout root is a two-column Grid.
- The two Expander controls are in a StackPanel in the right column of the Grid.
- The first Expander contains a set of Label controls inside a StackPanel.
- The second Expander (its Header is "2") contains a ScrollViewer. The ScrollViewer contains a StackPanel.

### HOW'D YOU DO?

It doesn't matter if your layout is a bit different from mine, as long as the basic structure is the same. (And even that can be different, as long as the window looks the same. It's the result that counts.)

```
<Grid>
<Grid.ColumnDefinitions>
<ColumnDefinition Width="232" />
<ColumnDefinition Width="146*" />
</Grid.ColumnDefinitions>
<GroupBox Header="Group Box" Height="135" Margin="10,10"
Name="groupBox1" Width="200">
<StackPanel>
<RadioButton FontSize="18" IsChecked="True">Option 1</RadioButton>
<RadioButton FontSize="18">Option 2</RadioButton>
<RadioButton FontSize="18">Option 3</RadioButton>
</StackPanel>
</GroupBox>
<StackPanel Grid.Column="1" >
<Expander Header="Expander 1" HorizontalAlignment="Left" Margin="20,10,0,0"
Name="expander1" IsExpanded="False">
<StackPanel>
<Label FontSize="14">Item 1</Label>
<Label FontSize="14">Item 2</Label>
<Label FontSize="14">Item 3</Label>
<Label FontSize="14">Item 4</Label>
</StackPanel>
</Expander>
<Expander Header="2" Margin="10,10" Name="expander2" ExpandDirection="Right"
IsExpanded="False" Padding="10,0" >
<ScrollViewer Height="75" >
<StackPanel>
<Label FontSize="14">Item 1</Label>
<Label FontSize="14">Item 2</Label>
<Label FontSize="14">Item 3</Label>
<Label FontSize="14">Item 4</Label>
</StackPanel>
</ScrollViewer>
</Expander>
</StackPanel>
</Grid>
```

You haven't seen the RadioButton control. Did you get the syntax right? Well done if you did.

## BUTTONS

The final important branch of content controls are the buttons. Of course, you've been using the basic Button all through the book, and what you've been doing—adding code to the Click event—is the most common use of any kind of button. But it's time to put buttons in context. Here's the class hierarchy:

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_573_0.png)

We'll talk about Command objects in Chapter 18.

The ToggleButton maintains its state.

The RadioButton (almost) always travels in a pack. We'll see how that works in a page or two.

A CheckBox may not seem like a button, but it makes sense if you think of a “button” as anything that’s intended to be clicked.

### BUTTON CONTENTS

We've seen that the distinguishing characteristic of a ContentControl is that it defines a property called Content. The property is defined as an Object, and I've said that that means it can be anything. Let's use the familiar Button control to explore the implications of that.

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_574_0.png)

Here's a basic button. Its content is defined (in attribute syntax) as Content="I'm a basic button". You've created a lot of these.

This is still a basic button. Its content is defined using property syntax:

```
<Button>
<Image Source="Binoculars.png" />
</Button>
```

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_574_1.png)

It's kind of cool, but what does it do? We should add a label,...

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_574_2.png)

That's better. Now, I could have added the label to the image, but that's really doing it the hard way. And what if you want to re-use the image with different labels? Instead, the direct content of the Button is a StackPanel that contains the Image and the Label:

```
<Button>
<StackPanel>
<Image Source="Binoculars.png" />
<Label>More Details</Label>
</StackPanel>
</Button>
```

### RADIO BUTTON GROUPS

If you look back to the partial class diagram of the RadioButton on page 565, you'll see that the class adds only one property to the ToggleButton from which it descends: GroupName, which is defined as a String. Unlike other types of buttons that operate independently, RadioButtons interact within a group—only one button in the group can be selected at any given time.

There are two ways to create a RadioButton group. You can either nest them in the same container (usually, but not always a GroupBox), or you can explicitly assign the GroupName property to the same value.

### PUT ON YOUR THINKING HAT

Re-create this window, using any image you like. When you do, and you run it, test the behavior of the RadioButton and CheckBox objects. Both of them are in StackPanels inside a GroupBox, but they behave differently. How?

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_575_0.png)

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_575_1.png)

### HOW'D YOU DO?

You may have used different layout objects than I did, and your sizing may be different. That's fine.

```
<Grid>
<Grid.ColumnDefinitions>
<ColumnDefinition Width="231" />
<ColumnDefinition Width="200" />
</Grid.ColumnDefinitions>
<Grid.RowDefinitions>
<RowDefinition Height="222" />
<RowDefinition Height="Auto" />
</Grid.RowDefinitions>
<Button Height="193" HorizontalAlignment="Left" Margin="10,10,0,0" Width="184">
<StackPanel>
<Image Source="Binoculars.png" Height="150" />
<Label HorizontalAlignment="Center" >More Details</Label>
</StackPanel>
</Button>
<GroupBox Grid.Column="1" Margin="10,10,10,19" Header="Choose one" Padding="10,10" BorderBrush="Black">
<StackPanel>
<RadioButton>Breakfast</RadioButton>
<RadioButton>Lunch</RadioButton>
<RadioButton>Dinner</RadioButton>
</StackPanel>
</GroupBox>
<GroupBox Grid.Row="1" Grid.ColumnSpan="2" Padding="10,10" Margin="10,10" Header="Choose as many as you like">
<StackPanel Orientation="Horizontal">
<CheckBox Margin="10,0">Mel</CheckBox>
<CheckBox Margin="10,0">Mel</CheckBox>
<CheckBox Margin="10,0">No, Pick Me!</CheckBox>
</StackPanel>
</GroupBox>
</Grid>
```

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_576_1.png)

### TAKE A BREAK

Why don't you take a quick break before you complete the Review and we finish up the chapter with an examination of items controls?

How does the Window class differ from other content controls?

There are two ways to create a set of RadioButtons. What are they?

What property distinguishes content controls?

What are the two methods you can use to open a Window?

What property distinguishes a headered content control?

What happens when you nest checkboxes in a group box?

How do you nest multiple objects in a content control?

## ITEMS CONTROLS

The other important branch of the control hierarchy is the set of classes that descend from ItemsControl. Like a content control, an items control takes a single element of content, but that item is a collection, the Items property, which is a collection of UIElement objects. (UIElement is the base class for FrameworkElement.)

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_578_0.png)

| Class | Base Class |
|-------|------------|
| Control | FrameworkElement |

The Selector branch of the class hierarchy add the ability for the user to select one or more items from the Items collection.

| Class | Base Class | Properties | Methods | Events |
|-------|------------|------------|---------|--------|
| TreeView | ItemsControl | SelectedItem, SelectedValue, SelectedValuePath | ExpandSubtree, ItemContainerGenerator, ScrollIntoView | SelectedItemChanged |

| Class | Base Class | Properties |
|-------|------------|------------|
| ItemsControl | Control | AlternationCount, HasItems, IsGrouping, IsTextSearchCaseSensitive, IsTextSearchEnabled, ItemContainerGenerator, Items, LogicalChildren |

| Class | Type | Base Class | Properties | Events |
|-------|------|------------|------------|--------|
| Selector | Abstract Class | Control | IsSynchronizedWithCurrentItem, SelectedIndex, SelectedItem, SelectedValue, SelectedValuePath | SelectionChanged |

Menus and toolbars also descend from Selector. We'll look at those in the next chapter.

| Class | Base Class | Properties |
|-------|------------|------------|
| TabControl | Selector | SelectedContent, TabStripPlacement |

| Class | Base Class | Properties | Methods |
|-------|------------|------------|---------|
| ListBox | Selector | SelectedItems | ScrollIntoView, SelectAll, UnselectAll |

| Class | Base Class | Properties | Events |
|-------|------------|------------|--------|
| ComboBox | Selector | IsDropDownOpen, IsEditable, IsReadOnly, IsSelectionBoxHighlighted, MaxDropDownHeight, SelectionBoxItem, SelectionBoxItemStringFormat, SelectionBoxItemTemplate, StaysOpenOnEdit, Text | DropDownClosed, DropDownOpened |

A ListView allows its list to be displayed in different ways. (Think about the items pane of the Windows Explorer.) This is done using templates and styles, which we'll discuss in Chapter 20 and 21.

| Class | Base Class | Properties |
|-------|------------|------------|
| ListView | ListBox | View |
