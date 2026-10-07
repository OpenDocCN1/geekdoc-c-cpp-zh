
# GridSplitter 46

```xml
<ColumnDefinition Width="*" />
<ColumnDefinition Width="*" />
<ColumnDefinition Width="*" />
</Grid.ColumnDefinitions>
<RowDefinitions>
<RowDefinition Height="*" />
<RowDefinition Height="*" />
<RowDefinition Height="*" />
</Grid.RowDefinitions>
<GridSplitter Grid.Column="1" Grid.RowSpan="10"
HorizontalAlignment="Left"
VerticalAlignment="Stretch"
Background="Blue"
ShowsPreview="False"
Width="5" />
<GridSplitter Grid.Column="1" Grid.RowSpan="10"
HorizontalAlignment="Right"
VerticalAlignment="Stretch"
Background="Red"
ShowsPreview="False"
Width="5" />
</Grid>
```

The following code creates horizontal GridSplitters for the same Grid used in the previous example:

```xml
<Grid>
<Grid.ColumnDefinitions>
<ColumnDefinition Width="*" />
<ColumnDefinition Width="*" />
<ColumnDefinition Width="*" />
</Grid.ColumnDefinitions>
<RowDefinitions>
<RowDefinition Height="*" />
<RowDefinition Height="*" />
<RowDefinition Height="*" />
</Grid.RowDefinitions>
<GridSplitter Grid.Row="1" Grid.ColumnSpan="20"
HorizontalAlignment="Stretch"
VerticalAlignment="Top"
Background="Blue"
ShowsPreview="False"
Height="5" />
<GridSplitter Grid.Row="1" Grid.ColumnSpan="20"
HorizontalAlignment="Stretch"
VerticalAlignment="Bottom"
Background="Red"
ShowsPreview="False"
Height="5" />
<Image Source="baseball.jpg" Grid.Row="1" Grid.Column="1" />
</Grid>
```

# MAKE ROOM

Be sure to allow room for the splitters when you place other objects inside the Grid. For example, if you place a 5-pixel-wide GridSplitter on the left edge of the second-column, then any other controls in column should have a left margin of at least 5 so they don't overlap with the splitter.

# LISTBOX

The ListBox displays a list of items and lets the user select one or more.

The control should contain ListBoxItems that holds the choices. The SelectedIndex, SelectedItem, and SelectedValue properties let you get and set the currently selected item.

**TABLE D-14**: Key Properties of ListBox

| PROPERTY | PURPOSE |
| --- | --- |
| HorizontalContentAlignment | Determines the ListboxItems are aligned. This can be Center, Left, Right, or Stretch. |
| SelectedIndex | Determines the index of the currently selected item. |
| SelectedItems | Returns the currently selected items. (You cannot use SelectedIndex, SelectedItem, or other selection properties to see which items are selected if more than one is.) |
| SelectionMode | Determines how many items the user can select. This can be Single (one item only), Multiple (can select multiple items by clicking on them individually), or Extended (can use [Shift]+click and [Ctrl]+click to select multiple items). |

**TABLE D-15**: Key Events for ListBox

| EVENT | PURPOSE |
| --- | --- |
| SelectionChanged | Occurs when the selected items change. |

The ListBox objects inside a ListBox also provide some useful events (see Table D-16).

# TABLE D-16:

| EVENT | PURPOSE |
|---|---|
| Selected | Occurs when the item is selected. |
| Unselected | Occurs when the item is unselected. |

# EXAMPLE Using ListBox

The following XML code builds a ListBox that lists the names of the solar system's planets. It also displays a Label that shows the name of the currently selected planet.

```xml
<StackPanel>
  <ListBox Names="listPlanets" SelectedIndex="2">
    <ListBoxItem Content="Mercury" />
    <ListBoxItem Content="Venus" />
    <ListBoxItem Content="Earth" />
    <ListBoxItem Content="Mars" />
    <ListBoxItem Content="Jupiter" />
    <ListBoxItem Content="Saturn" />
    <ListBoxItem Content="Uranus" />
    <ListBoxItem Content="Neptune" />
    <ListBoxItem Content="Pluto" />
  </ListBox>
  <Label Content="{Binding ElementName=listPlanets, Path=SelectedItem.Content}"/>
</StackPanel>
```

# MENU

The Menu displays a menu for a Window. While you can place controls such as Labels, Buttons, and TextBoxes in a Menu, a Menu normally holds MenuItem objects that contain the Window's top-level menus (see Tables D-17 through D-19).

A MenuItem's Header property determines what it displays. A MenuItem can contain other MenuItems to build a menu hierarchy.

# TABLE D-17:

| PROPERTY | PURPOSE |
|---|---|
| IsMainMenu | Determines whether the control is the main menu. If a Window contains more than one menu, all other menus should set this to False so they are not notified when the user presses the [Alt] key or [F10]. |

# APPENDIX D USER INTERACTION CONTROLS

TABLE D-18:
| PROPERTY | PURPOSE |
|---|---|
| Command | Determines the command associated with the menu item. |
| CommandParameter | Determines the parameter passed to a Command. |
| CommandTarget | Determines the object on which to raise a Command. |
| IsCheckable | Determines whether the menu item can be checked. If this is True, then the item automatically checks and unchecks itself. |
| IsChecked | Determines whether the control is currently checked. |
| IsSubOpen | Determines whether the menu is open. |

TABLE D-19:
| EVENT | PURPOSE |
|---|---|
| Checked | Occurs when the control is checked. |
| Click | Occurs when the control is clicked. |
| SubmenuOpened | Occurs when the submenu is opened. |
| Unchecked | Occurs when the control is unchecked. |

# EXAMPLE Using Menu

The following XML code builds a Menu with several MenuItems.

```xml
<Menu>
  <MenuItem Header="File">
    <MenuItem Header="New" />
    <MenuItem Header="Open" />
  </MenuItem>
  <MenuItem Header="Edit">
    <MenuItem Header="Copy" />
    <MenuItem Header="Paste" />
  </MenuItem>
</Menu>
```

# PASSDBOX

The PasswordBox is a textbox that hides its text on the screen, displaying a dot, asterisk, or other character for each character (see Table-21).

TABLE D-20: Key Properties of PasswordBox

| PROPERTY | PURPOSE |
|---|---|
| Password | Determines the current password in plaintext. |
| PasswordChar | Determines the character displayed when entered. |
| SecurePassword | Returns the current password as SecureString. |

TABLE D-21: Key Events for PasswordBox

| EVENT | PURPOSE |
|---|---|
| PasswordChanged | Occurs when the password changes. |

# EXAMPLE Using Password

The following code creates two PasswordBoxes. The first uses the default font and PasswordChar so it displays a circle. The second uses the Wingdings font with PasswordChar="N".

```xml
<PasswordBox Password="Secret" />
<PasswordBox Password="Secret" FontFamily="Wingdings" PasswordChar="N" />
```

# RADIOBUTTON

The RadioButton lets the user select one of an exclusive set of options (see Table D-22). When the user selects one RadioButton, all others in the same container are deselected. (Contrast with the CheckBox, where any number can be selected at a time.)

### NEVER COMBO
Note that the ComboBox also lets the user select one of a series of choices so you could consider using a ComboBox instead of a group of RadioButtons, particularly if you need to save space.

You can create multiple RadioButton groups by placing them in different containers or by using the GroupName property.

TABLE D-22:
| PROPERTY | PURPOSE |
|--- |--- |
| IsChecked | Determines whether the control is currently checked. |
| GroupName | Defines RadioButton groups. RadioButtons that share the same non-null GroupName value are part of the same group, even if they lie in different containers. |
| IsThreeState | Determines whether the control cycles through three values — checked (IsChecked = True), unchecked (IsChecked = False), and indeterminate (IsChecked = null). |

Only code can set a RadioButton to an indeterminate state. The user can only check or uncheck a RadioButton.
When a RadioButton is in an indeterminate state, it doesn't uncheck if the user checks a different RadioButton in the same group (see Table D-23).

TABLE D-23:
| EVENT | PURPOSE |
|---| |---|
| Checked | Occurs when the control is checked. |
| Unchecked | Occurs when the control is unchecked. |
| Click | Occurs when the control is checked or unchecked. |
