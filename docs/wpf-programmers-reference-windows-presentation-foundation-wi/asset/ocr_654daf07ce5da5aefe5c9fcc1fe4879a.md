Now use the appropriate CanExecute and Exec routines in the code-behind. The ImageColors program uses the following CanExecute routine for all of commands so they are all enabled when the window's checkbox is checked:

```
// Return True if the CheckBox is checked.
private void CanExecuteChecked(Object sender, CanExecuteRoutedEventArgs e)
{
    e.CanExecute = (checkBox.IsEnabled == true);
}
```

![](bbox=[0.095, 0.13, 0.155, 0.24])

![](bbox=[0.835, 0.24, 0.935, 0.26])

The Invert command's Exec method is interesting but not relevant to this discussion, so it isn't shown here. Develop the example command from the book's web to see how it works.

In the next XML code, add command bindings to tell the program which routines to use for the command's CanExecute and Exec properties. The following code shows how the ImageColors program binds its Invert command:

```
<Window.CommandBindings>
  <CommandBinding Command="{x:Static local:Window1.CommandInvert}"
                  CanExecute="{Binding ExecuteCommandChecked}"
                  Exec="{Binding ExecuteImageInvert}"/>
  <!-- Code for other commands omitted -->
  </CommandBinding>
</Window.CommandBindings>
```

![](bbox=[0.095, 0.42, 0.155, 0.53])

![](bbox=[0.835, 0.495, 0.935, 0.51])

Finally, add the XAML code to display the buttons, menu items, and other controls that invoke the command.

The following code shows how the ImageColors program displays its Invert menu item. The MenuItem control automatically the command's Text property to display its caption. It uses the command's input gesture to display the shortcut [Alt+I].

```
<MenuItem Command="{x:Static local:Window1.CommandImageInvert}" />
```

The following code shows how the program displays its Invert button. Unlike the corresponding menu item, the button does not automatically get its caption from the command object, so the XAML code must use the button's caption.

```
<Button Name="btnInvert"
             Command="{x:Static local:Window1.CommandImageInvert}"
             Style="{StaticResource ButtonStyle}"
             Content="{Binding RelativeSource={RelativeSource Self}, Path=Command.Text} />
```

![](bbox=[0.095, 0.74, 0.155, 0.85])

![](bbox=[0.835, 0.82, 0.935, 0.84])

Now explain how the code binds the button's Content to the command object's Text property. Because the code-behind added the underscore to the object's text, the button automatically underlines an accelerator when you press the [Alt] key and responds to the [Alt]+I key sequence.