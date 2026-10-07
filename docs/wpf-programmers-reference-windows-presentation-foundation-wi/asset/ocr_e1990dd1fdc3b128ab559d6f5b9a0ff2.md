to see which of the menu items should be enabled. For example, if the user has not undone a command,
recently, then CanDo returns False and the mnuEditRedo menu is disabled.

```
// Enable or disable the Undo and Redo commands.
private void mnuEditSubmenuOpened(object sender, RoutedEventArgs e)
{
    mnuUndo.IsEnabled = (richTextBox.CanUndo);
    mnuEditRedo.IsEnabled = (richTextBox.CanRedo);
}
```

The following code shows how the program invokes the control's Undo and Redo methods.

```
// Undo.
private void mnuEditUndo_Click(object sender, RoutedEventArgs e)
{
    richTextBox.Undo();
}
```

```
// Redo.
private void mnuEditRedo_Click(object sender, RoutedEventArgs e)
{
    richTextBox.Redo();
}
```

# Other Features

The RichTextBox control provides many other features to mention them all here. Before moving on, however, the following table summarizes some key RichTextBox properties.

| PROPERTY | PURPOSE |
|---|---|
| AcceptsReturn | Determines whether [Enter] key strokes are placed in the control's content or whether they are sent to the window. If AcceptsReturn is False and the window contains a Button with IsDefault is True, then pressing [Enter] inside the controls the Button. |
| AcceptsTab | Determines whether [Tab] key strokes are placed in the control's content or whether they are sent to the window. If AcceptsTab is False, then pressing [Tab] moves focus to the window's next control. |
| HorizontalScrollBarVisibility | Determines whether the horizontal scrollbar is visible. It can be Auto, Disabled, Hidden, or Visible. |