Like the MenuItems, the toolbar the Buttons properties set to the name of the commands they execute. Unlike MenuItems, however Buttons do not automatically display the commands' text and shortcut keys, the program includes XAML code that sets the Buttons' text.

Each Button's Content property is set to a binding that makes WPF like the Button, get its Command property, and that makes the Button display the appropriate text for commands.

# SETTING BUTTON TEXT

> You could set Button's Text explicitly to Copy, Cut, and so forth, but it would add an extra chance to introduce bugs with the text not matching the command's name.

Left to its own devices, commands like ApplicationCommands.Copy enable their sources when any appropriate control makes the operation possible. For example, the Copy command activates its controls when the textbox has the focus selected.

If you want, you can set a command's to tie it to a specific control, you can use a textbox as a button command. The command enables or disables its menu item, button, and other controls depending on whether text is selected in that particular textbox.

The CommandTarget example program shown in Figure 19-3 demonstrates command targets.

Many of the controls are similar to those used by the TextBox program. The program's Edit menu and contain Copy, Cut, Paste, and Redo items that you use the appropriate predefined ApplicationCommands.

The program also provides Copy, Cut, and Paste buttons that have the upper textbox in Figure 19-3 as their command targets. Their commands enable and disable these controls depending on the text of that textbox.

The following code shows how the CommandTarget properties are set to the upper textbox txtTop.

```
<StackPanel Grid.Row="0" Grid.Column="1" Margin="0,0,5,0"
VerticalAlignment="Center">
  <!-- Introduce commands on txtTop. -->
  <Button Grid.Row="0" Grid.Column="1" Margin="2"
    Content="Binding RelativeSource={RelativeSelf}, Path=Command.Text"
    Command="ApplicationCommands.Copy"
    CommandTarget="Binding ElementName=txtTop"/>
  <Button Grid.Row="0" Grid.Column="1" Margin="2"
    Content="Binding RelativeSource={RelativeSelf}, Path=Command.Text"
    Command="ApplicationCommands.Cut"/>
```

![](bbox=[0.613, 0.516, 0.915, 0.706])

![](bbox=[0.093, 0.804, 0.173, 0.866])