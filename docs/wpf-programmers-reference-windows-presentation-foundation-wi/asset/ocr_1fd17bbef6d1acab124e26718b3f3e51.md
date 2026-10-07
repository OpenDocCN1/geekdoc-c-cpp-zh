The following XAML code builds the menu shown in Figure 7-9. Notice the Separator object between the "Save As" Alignment="Top".

```
<Menu VerticalAlignment="Top">
  <Menu HorizontalAlignment="Left" VerticalAlignment="Top" Header="File">
    <MenuItem Header="_New" InputGestureText="Ctrl+N/>
    <MenuItem Header="_Open" InputGestureText="Ctrl+O/>
    <MenuItem Header="_Save" InputGestureText="Ctrl+S/>
    <MenuItem Header="_Save As" InputGestureText="Ctrl+A/>
    <Separator/>
    <MenuItem Header="_Edit"/>
  </Menu>
  <Menu>
    <MenuItem Header="_Effects">
      ...MenuItem omitted
    </MenuItem>
  </Menu>
</Menu>
```

A MenuHeader is often plaintext but it can be any single control including a container. Each of the menu items shown in Figure 7-10 contains a horizontal StackPanel that holds an Image and a Label.

The MenuItems shown in Figure 7-10 also demonstrate two properties. The IsCheckable property determines whether the item can display a checkbox. The IsChecked property determines whether the item is actually checked. In Figure 7-10, every MenuItem has IsChecked = True, but only the "Drop Shadow" MenuItem has IsChecked = True.

The following code shows how the MenuExample program defines the "Drop Shadow" MenuItem shown in Figure 7-10:

```
<MenuItem IsCheckable="True" IsChecked="True">
  <MenuItem.Header>
    <StackPanel Orientation="Horizontal">
      <Image Stretch="None" Source="GraySmiley.bmp" Margin="0,0,20,0/>
      <Image.BitmapEffect>
        <DropShadowBitmapEffect/>
      </Image.BitmapEffect>
    </Image>
    <Label Content="_Drop Shadow"/>
  </StackPanel>
  </MenuItem.Header>
</MenuItem>
```

![](bbox=[0.655, 0.37, 0.925, 0.59])