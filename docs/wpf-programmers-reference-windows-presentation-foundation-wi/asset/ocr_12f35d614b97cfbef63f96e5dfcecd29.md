# TABLE D-16:

| EVENT | PURPOSE |
|---|---|
| Selected | Occurs when the item is selected. |
| Unselected | Occurs when the item is unselected. |

# EXAMPLE Using ListBox

The following XML code builds a ListBox that lists the names of the solar system's planets. It also displays a Label that shows the name of the currently selected planet.

```
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