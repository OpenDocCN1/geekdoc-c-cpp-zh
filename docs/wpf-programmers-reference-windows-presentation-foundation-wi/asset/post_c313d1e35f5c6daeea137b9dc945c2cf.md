
Two other useful properties are HorizontalContentAlignment and VerticalContentAlignment, which let you control how items in the list are aligned.

The UseBox example program in Figure 7-8 contains a ListBox with SelectionMode set to Extended and the third, fifth, and sixth items selected.

Each ListItem must contain a single child, but that child can be a container such as Grid, which can effectively put anything you want in the list.

The following XML code shows how the program builds this ListBox. The "Mountain Uncycling" item uses a StackPanel to contain a Text and an Image.

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_166_0.png)

```
<ListBox Row="1"
HorizontalAlignment="Stretch" VerticalAlignment="Stretch" Height="Auto"
IsSynchronizedWithCurrentItem="True"
FontSize="16" FontWeight="Bold"
Foreground="Blue" Background="Pink"
HorizontalContentAlignment="Left" VerticalContentAlignment="Top"
SelectionMode="Extended">
  <ListBox Content="Bassallo/"
  <ListBox Content="Ga-Ga/"
  <ListBox Orientation="Horizontal">
    <StackPanel>
      <TextBlock Text="Mountain Unycycling" VerticalAlignment="Center"/>
      <Image Source="Uncycling.jpg" Stretch="Uniform" Height="50" Margin="3,0,0,0"/>
    </StackPanel>
  </ListBox>
  <ListBox Content="Pessallo/"
  <ListBox Content="Hornnussen/"
  <ListBox Content="Trugo/"
</ListBox>
```

FIGURE 7-8

# COLOR CAUTION

The ListBox controls how an item's color changes when it is selected. To ensure that the user can select an item when it is selected, don't cover the entire item with a control that has explicitly set foreground and background colors.

For example, in the previous code, if you set the StackPanel's Background to red and the TextBlock's Foreground to black, it's harder to tell when the Mountain Unycycling item is selected.

To make it easier for the ListBox to change items' colors, the control doesn't inherit its background color from its container.

# MENU

The Menu control displays a main menu for a window. The Menu can provide submenus, shortcuts (such as [Ctrl]+O for the Open command), and accelerators (e.g., opening the File menu when you press [Alt]+F).

The Menu contains MenuItem objects that represent the commands in the menu. You can build submenus by placing MenuItems inside other MenuItems.

When the user selects a menu item, the corresponding MenuItem object raises its Click event. Your program can catch and handle that event as it handles Button Click.

The MenuItem's Header property determines what it displays. The Header value is simple text. Place an ampersand in front of the Header's letter that you want the MenuItem to use as an accelerator. For example, if you set the Header to File, then the MenuItem displays File (Note that this is different from the way Windows Forms handles this. In a Windows Forms application, you place an ampersand in front of the character that you want to underline in a menu).

# ACTIVATING ACCELERATORS

In recent Windows operating systems, accelerator characters are not normally underlined until the user presses the [Alt] key. Then the accelerator characters are underlined, and the user can press the corresponding key to trigger it.

In a typical application, for example, when the user presses [Alt], the File menu's underline appears. If the user presses F, the menu shows its items with accelerator keys underlined. In many programs, the File menu contains a New command. If the user presses N while the accelerators are visible, that command executes.

To set a menu item's shortcut keys by using the MenuItem's InputGestureText property. For example, you set the InputGestureText for the New command to [Ctrl]+N.

Support for accelerators is automatic. You only need to define the accelerator by adding underscores, and the application automatically does the rest.

Unfortunately, support for shortcuts is not automatic, your program must catch the appropriate keystroke and take action when necessary. WPF provides a command architecture that allows you to handle shortcuts for menu items in a general way, but since it is fairly complicated, it isn't described in any more detail here. Chapter 19, "Commanding," covers commands completely.

Figure 7-9 shows a program with its File menu. In this figure, I pressed [Alt] and F to open the File menu.

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_167_0.png)

FIGURE 7-9

The following XAML code builds the menu shown in Figure 7-9. Notice the Separator object between the "Save As" Alignment="Top".

```
<Menu VerticalAlignment="Top">
  <Menu HorizontalAlignment="Left" VerticalAlignment="Top" Header="File">
    <MenuItem Header="_New" InputGestureText="Ctrl+N"/>
    <MenuItem Header="_Open" InputGestureText="Ctrl+O"/>
    <MenuItem Header="_Save" InputGestureText="Ctrl+S"/>
    <MenuItem Header="_Save As" InputGestureText="Ctrl+A"/>
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
      <Image Stretch="None" Source="GraySmiley.bmp" Margin="0,0,20,0"/>
      <Image.BitmapEffect>
        <DropShadowBitmapEffect/>
      </Image.BitmapEffect>
    </Image>
    <Label Content="_Drop Shadow"/>
  </StackPanel>
  </MenuItem.Header>
</MenuItem>
```

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_168_0.png)

# UNLIMITED FREE CHECKING

Support for checkable items is almost automatic in WPF. If a MenuItem has IsCheckable = True, then the program will automatically check the item when the user clicks it. The MenuItem even provides Checked and Unchecked events to let the program know what's happening.

If all you need is the item, you're done. If you need menu items to be exclusive (e.g., you only want one of the items shown in Figure 7-10 to be checked at a time), you need to add extra code to uncheck the other items when an item is checked.

# MENUS, MENUS EVERYWHERE

Normal menus stretch across the top of an application, but there's nothing to prevent you from putting them in other places. For example, you could add a menu inside a GroupBox or in the tabs of a TabControl to provide commands that only apply to the controls. You could even apply transformations to menus to make them rotated or skewed.

Have on your users, and don't go crazy menus over the place. If you make the menus too confusing, you'll have to spend a lot of time explaining things to confused users.

One final point is worth mentioning. You can set a MenuItem's Icon property to determine the picture that is displayed to it while the item is not checked. When the item is checked, it shows a checkmark similar to the one next to the “Drop Shadow” in Figure 7-10 to replace the Icon.

# PASSWORDBOX

A Password is a relatively simple textbox that replaces the characters that users type with dots (•) or some other special character on the screen. Internally the control keeps track of what's being typed but prevents the user from seeing it. To the point, it prevents Phil the prankster from peeking over the user's shoulder to see the password.

The UsePasswordBox example program shown in Figure 7-11 demonstrates the PasswordBox. Enter a username and password. As you type the password, the PasswordBox displays a series of dots. When you click the OK button, the program displays the username and password that you entered.

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_169_0.png)
