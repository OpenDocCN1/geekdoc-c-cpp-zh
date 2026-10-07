# 294 | CHAPTER 16 THEMES AND SKINS

```
Foreground="Blue"
Clicks="ctxSkin_Click Tag=ResBlue.xaml/>
</ContextMenu>
</Label.ContextMenu>
</Label>
```

Skins

This code contains four points of interest:

+   1. First, the Label's MouseDown event triggers the Options_MouseDown event handler. This routine, which is shown in the following code, displays the context menu by setting the ContextMenu.IsOpen property to True:

```
// Display the options context menu.
private void Options_MouseDown(object sender, RoutedEventArgs e)
{
    ctxOptions.IsOpen = true;
}
```

![](bbox=[0.042, 0.303, 0.115, 0.366])

Skins

+   2. Second, the Label's Visibility property is set to the value of the blue static resource. This resource has the value True in the blue dictionary and False in the Red dictionary. This means that the Label is only visible in the blue interface. The interface's skin-changing image uses a similar visRed resource that is only True in the red interface.

+   3. Third, the context menu items have a Tag property that matches the XAML resource file they load. For example, the blue menu item has its Tag set to ResBlue.xaml. The program uses the Tag property to figure out which file to load when the users pick a menu item.

+   4. Finally, both of the context menu items fire the ctxSkin_Click event handler when selecting the skin. Use the following code to load the skin:

![](bbox=[0.042, 0.623, 0.115, 0.686])

```
// Use the selected skin.
private void ctxSkin_Click(object sender, RoutedEventArgs e)
{
    // Get the context menu item that was clicked.
    MenuItem menu_item = (MenuItem)sender;

    // Create a new resource dictionary, using the
    // menu item's Tag property as the dictionary URI.
    ResourceDictionary dict = new ResourceDictionary();
    dict.Source = new Uri((String)menu_item.Tag, UriKind.Relative);

    // Remove all but the first dictionary.
    while (App.Current.Resources.MergedDictionaries.Count > 1)
    {
        App.Current.Resources.MergedDictionaries.Remove(1);
    }
    // Install the new dictionary.
    App.Current.Resources.MergedDictionaries.Add(dict);
}
```

Skins