The function LoadSkin uses the following code to load a XAML skin file. To save space, the code shows a few of the statements that controls to their event handlers.

```
// Load the skin file and wire up event handlers.
private void LoadSkin(string skin_file)
{
    // Load the controls.
    FrameworkElement element =
        (FrameworkElement)Application.LoadComponent(
            new Uri(skin_file, UriKind.Relative));
    this.Content = element;

    // Wire up the event handlers.
    Button btn;
    Polygon pgn;
    Rectangle rect;
    Grid grd;
    Ellipse ell;

    switch (element.ToString())
    {
        case "Red":
            btn = (Button)element.FindName("btnRepairDisk");
            btn.Click += new RoutedEventHandler(btnRepairDisk_Click);

            // Code for other controls omitted
            break;
        case "Blue":
            Lots of code omitted

            // Uses the same event handler as rectMove.
            ell = (Ellipse)element.FindName("ellMove");
            ell.MouseDown += new.Windows.Input.MouseEventHandler(
                rectMove_MouseDown);

            grd = (Grid)element.FindName("grdExit");
            grd.MouseDown += new.Windows.Input.MouseEventHandler(
                grdExit_MouseDown);
            break;
    }
```

SkinInterfaces

The code starts by using the WPF Component method to load the desired XAML skin file. It sets the Window's main content to the root element from the file so the controls are displayed.

Next, the code checks the newly loaded element's Tag property to see whether it is now displaying the red or the blue skin. Depending on which skin is loaded, the code looks for specific controls in the skin and connects their event handlers.