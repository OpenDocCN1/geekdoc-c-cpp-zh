# 626 Commanding Attention

The sample shown in Listing 4-2 and Figure 4-1 uses the ApplicationCommands.Copy and ApplicationCommands.Paste commands to facilitate clipboard manipulation in your application. When the UIElement with focus supports the clipboard Paste action and there is data in the clipboard that is support by the element, any elements bound to the Paste command are enabled. When the UIElement with focus supports the clipboard Copy and there are items that can be copied to the clipboard, elements bound to them the Copy command are enabled. (See Figures 4-2 and 4-3.) As a side note, WPF allows you to abbreviate the built-in commands by dropping the container name (ApplicationCommands), so Copy and Paste are legitimate abbreviations for the command bindings ApplicationCommands.Copy and ApplicationCommands.Paste. For readability, I prefer to fully qualify the names.

The full code for the Command sample is in the project Chapter 4Commands and Chapter4CommandsTests in the Chapter 4 Solution.

# Listing 4-2: Built-in commands in XAML

```
<Menu Grid.Row="0" Grid.Column="0" HorizontalAlignment="Left" Name="menu">
  <MenuItem Command="ApplicationCommands.Copy/>
  <MenuItem Command="ApplicationCommands.Paste"/>
</Menu>
<TextBox Grid.Row="1" Grid.Column="0" HorizontalAlignment="Stretch"/>
<TextBox Grid.Row="2" Grid.Column="0" HorizontalAlignment="Stretch"/>
```

**Figure 4-1:
Built-in commands (with empty clipboard and no selections).

![](bbox=[0.25, 0.613, 0.443, 0.663])

**Figure 4-2:
Built-in commands (with empty clipboard and text selection).

![](bbox=[0.25, 0.795, 0.443, 0.845])