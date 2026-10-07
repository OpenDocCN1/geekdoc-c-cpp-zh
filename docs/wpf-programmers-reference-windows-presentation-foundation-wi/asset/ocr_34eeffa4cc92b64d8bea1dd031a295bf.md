This technique is much more useful on the few occasions upon which you do want multiple copies of the same content. For example, suppose an application displays a series of pictures of people and you want to provide each with the same menu context: Details, Email, Phone, and Delete. Deleting the code defines a ContextMenu that includes these commands and a BitmapEffect that drops shadows:

```
<Window.Resources>
  <ContextMenu x:Key="ctxPerson">
    <MenuItem Header="Details" Click="mnuDetails_Click"/>
    <MenuItem Header="Email" Click="mnuEmail_Click"/>
    <MenuItem Header="Phone" Click="mnuPhone_Click"/>
    <Separator/>
    <MenuItem Header="Delete" Click="mnuDelete_Click"/>
  </ContextMenu>
  <BitmapEffectGroup x:Key="bmePerson">
    <DropShadowBitmapEffect/>
  </BitmapEffectGroup>
</Window.Resources>
```

The following code shows how an Image can use the resources:

```
<Image Name="imgClaude" Width="100" Height="100" Stretch="Uniform"
MouseDown="img_MouseDown"
Source="Claude.jpg" Tag="Claude"
BitmapEffect="(StaticResource bmePerson)"
ContextMenu="(StaticResource ctxPerson)"/>
```

A series of Buttons can use similar code to display the same ContextMenu.
The program uses code-bind to respond when the user selects a context menu MenuItem.
Unfortunately the Click event handler raised by the MenuItem doesn't know which Image control the user clicked. The MenuItem's parameters tell which MenuItem was clicked but not which Image displayed the Context.

One way to figure out which Image displayed the menu is to save a reference to Image when the menu is displayed. The ContextMenu example program assigns the following event handler to all of its Image controls' MouseDown event handlers. If the user is pressing the right button over the Image, then the code saves a reference to the Image control for use when the user selects a menu item.

```
// Remember the image clicked.
private Image m_ImageClicked = null;
private void img_MouseDown(Object sender, MouseButtonArgs e)
{
  if (e.RightButton == MouseButtonState.Pressed)
  {
    m_ImageClicked = (Image)sender;
  }
}
```