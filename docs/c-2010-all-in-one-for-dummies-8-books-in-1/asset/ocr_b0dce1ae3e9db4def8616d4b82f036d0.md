# 604 Commanding Attention

Listing 4-2: Built-in Commands in XAML

```
<Menu Grid.Row="0" Grid.Column="0" HorizontalAlignment="Left"
Name="menu">
  <MenuItem Command="ApplicationCommands.Copy"/>
  <MenuItem Command="ApplicationCommands.Paste"/>
</Menu>
<TextBox Grid.Row="1" Grid.Column="0"
HorizontalAlignment="Stretch"/>
<TextBox Grid.Row="2" Grid.Column="0"
HorizontalAlignment="Stretch"/>
```

Figures 4-1 through 4-3 show the Window produced by the XAML in Listing 4-2 different states. When there is text selected in a text box, the Copy menu is enabled. When there is data in the clipboard that can be pasted into a text box, the Paste menu becomes enabled. This is all done without a single line of code!

Figure 4-1: Built-in commands (with empty clipboard and no selections).

![](bbox=[0.24, 0.456, 0.442, 0.513])

Figure 4-2: Built-in commands (with empty clipboard and text selection).

![](bbox=[0.24, 0.635, 0.442, 0.692])

Figure 4-3: Built-in commands (with clipboard data and no text selection).

![](bbox=[0.24, 0.83, 0.442, 0.887])