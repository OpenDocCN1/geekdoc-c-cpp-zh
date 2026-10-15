C#) for the application. In the App.xaml file, you can specify the required XML namespaces, the startup file for the application, and resources. By default, the App.xaml file appears as given in Listing 9.2:

# Listing 9.2: Displaying the Contents of the App.xaml File of a Standalone WPF Application

```
<Application x:Class="WpfApplication1.App"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    StartupUri="MainWindow.xaml">
    <Application.Resources>
    </Application.Resources>
</Application>
```

In Listing 9.2, the App.xaml file has names written within the angular brackets (< >), similar to other markup languages, such as HTML and XML. The names within the angular brackets are the tags or markup elements in XAML. The first markup element in the App.xaml file is the <Application> element that corresponds to the Application class. In addition, the Application class is the main class that offers commonly used services and features of a WPF application to assist you in properly managing the WPF application. You learn about the Application class later in this chapter.

Let's now look at the MainWindow.xaml and MainWindow.xaml.cs files that are displayed in the Solution Explorer. These two files collectively correspond to the default window of the WPF 4.0 applications. Listing 9.3 shows the default content of the MainWindow.xaml file:

# Listing 9.3: Default Content of the MainWindow.xaml File in the WpfApplication1 Application

```
<Window x:Class="WpfApplication1.MainWindow"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    Title="MainWindow" Height="350" Width="525">
    <Grid>
    </Grid>
</Window>
```

In Listing 9.3, the <Window> element of XAML represents a window in standalone WPF 4.0 applications. The <Window> element is the topmost element in the MainWindow.xaml file. It is associated with the MainWindow partial class in the MainWindow.xaml.cs file. The application logic related to the window is specified in the MainWindow partial class.

# The Window Class

In standalone WPF 4.0 applications, the entire content of an application is contained in one or more windows. A window is a rectangular region on the UI (similar to a form in Windows Forms applications) that allows you to display the contents of a WPF application. A window has a border, a title, and buttons, such as Maximize, Minimize, and Close. WPF windows also have a menu that offers options to move and resize a window. Note that you can see the Maximize, Minimize, and Close buttons and the menu only at run time and not at design time.

WPF windows are instances of the Window class, which has the following class hierarchy:

```
System.Object
  System.Windows.Threading.DispatcherObject
    System.Windows.DependencyObject
      System.Windows.Media.Visual
        System.Windows.UIElement
          System.Windows.FrameworkElement
            System.Windows.Controls.Control
              System.Windows.Controls.ContentControl
                System.Windows.Window
```

The Window class offers many properties and methods that allow you to work with windows in a WPF application. Table 9.1 lists some of the noteworthy properties of the Window class:

# Table 9.1: Noteworthy Properties of the Window Class

| Property | Description |
|---|---|
| AllowsTransparency | Sets or retrieves a value that indicates whether or not the window can be transparent |