In this case, you want to set the DataContext to an object that has already been instantiated. Modify the App.xaml file so that it looks as shown in Listing 18.2.

# **LISTING 18.2** Application XAML

```
<Application x:Class="PhotoViewer.App"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    Startup="OnApplicationStartup">
   <Application.Resources> </Application.Resources>
</Application>
```

Then, in the App.xaml.cs, add the event handler method, as shown in Listing 18.3.

# **LISTING 18.3** The OnApplicationStartup Event Handler

```
void OnApplicationStartup(object sender, StartupEventArgs args)
{
    MainWindow mainWindow = new MainWindow();
    mainWindow.Show();
    this.MainWindow.DataContext = mainWindow.Photos;
}
```

In addition to setting the DataContext, you can also specify the binding source by setting the Source property of the binding. You can also use the ElementName property, which is useful when you want to bind to other elements in your application. When you specify the binding as part of a control template or a style, the RelativeSource property is useful as well.

# Try It Yourself

# **Adding Data Binding to the PhotoViewer Application**

By following these steps, you add data binding to the PhotoViewer application.

+   1. If you haven’t already done so, modify the App.xaml and App.xaml.cs files to look as shown in Listing 18.2 and Listing 18.3, respectively.

2. Modify the Button_Click event handler to what is shown in Listing 18.1.

3. In MainWindow.xaml, add a binding for the Content property of the ImagesDirectory label so that it is bound to the Path property of mainWindow.Photos.

4. For each of the Label controls in the details StackPanel, add a binding for the Content property to the appropriate property of the Photo class. The Label