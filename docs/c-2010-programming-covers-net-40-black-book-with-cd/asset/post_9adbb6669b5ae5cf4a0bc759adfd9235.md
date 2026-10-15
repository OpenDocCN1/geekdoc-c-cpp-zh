
## Figure 9.9: Creating a Standalone WPF 4.0 Application

In Figure 9.9, you can see that the designer interface of a standalone WPF application is similar to that of a Windows Forms application. For instance, there are certain tools available in the Toolbox and a form-like structure called window at the center.

You learn about the designer interface of WPF applications later in this chapter. Let’s now explore the initial files required to create standalone applications.

## Files for Standalone WPF Applications

You can explore the different files that constitute standalone WPF applications by opening the Solution Explorer, and expanding the References, App.xaml and MainWindow.xaml nodes, as shown in Figure 9.10:

## Figure 9.10: Displaying the File Structure of Standalone WPF 4.0 Applications

Under the References node, you can view the essential .NET namespaces and assemblies, such as PresentationCore, PresentationFramework, and WindowsBase. When you expand the App.xaml node, you can view the respective code-behind file, App.xaml.cs. The App.xaml and App.xaml.cs files collectively represent the entire WPF application. The App.xaml file is an XAML file, while the App.xaml.cs file is the code-behind file (in

![](img/e073a4882197be4ab61103cbe0bcb394_351_0.png)

![](img/e073a4882197be4ab61103cbe0bcb394_351_1.png)

C#) for the application. In the App.xaml file, you can specify the required XML namespaces, the startup file for the application, and resources. By default, the App.xaml file appears as given in Listing 9.2:

## Listing 9.2: Displaying the Contents of the App.xaml File of a Standalone WPF Application

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

## Listing 9.3: Default Content of the MainWindow.xaml File in the WpfApplication1 Application

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

## The Window Class

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

## Table 9.1: Noteworthy Properties of the Window Class

| Property | Description |
|---|---|
| AllowsTransparency | Sets or retrieves a value that indicates whether or not the window can be transparent |
| DialogResult | Sets or retrieves the result of a dialog box, for example, the result of clicking the OK or Cancel button |
| Height | Sets or retrieves the height of the window |
| Icon | Sets or retrieves the icon of the window |
| IsActive | Retrieves a value that indicates whether or not the window is active, that is, whether the window is on top of all the other windows in an application |
| Left | Sets or retrieves the current position of the left side or edge of the window with respect to the screen |
| LogicalChildren | Retrieves an enumerator with the logical child elements of the window |
| Name | Sets or retrieves the name of the window |
| OwnedWindows | Retrieves the collection of windows that are owned by the current window |
| Owner | Sets or retrieves the owner window for the current window |
| ResizeMode | Sets or retrieves a value from the ResizeMode enumeration to specify whether or not the window can be resized |
| RestoreBounds | Retrieves the size and position of the window when it is restored |
| ShowInTaskbar | Allows you to specify whether the window appears in the taskbar |
| SizeToContent | Sets or retrieves a value from the SizeToContent enumeration to specify whether the window resizes itself automatically to accommodate the content |
| Title | Sets or retrieves the title of the window |
| Top | Sets or retrieves the current position of the top side or edge of the window with respect to the screen |
| Topmost | Sets or retrieves a value that indicates whether or not the window always appears on top of other windows |
| Width | Sets or retrieves the width of the window |
| WindowStartupLocation | Sets or retrieves the startup position of the window |
| WindowState | Sets or retrieves the current state of window, that is, whether the window is minimized, maximized, or restored |
| WindowStyle | Sets or retrieves the current style of the border of the window |

Table 9.2 lists the noteworthy methods of the Window class:

## Table 9.2: Noteworthy Methods of the Window Class

| Method | Description |
|---|---|
| Activate | Activates the window by displaying it in the foreground |
| AddChild | Adds a control or element as a child to the window |
| Close | Closes the window |
| DragMove | Allows you to move the window by pressing the left mouse button and dragging the mouse |
| GetWindow | Retrieves the window that hosts a given dependency object |
| Hide | Hides the window |
| OnClosed | Raises the Closed event for the window |
| OnClosing | Raises the Closing event for the window |
| OnLocationChanged | Raises the LocationChanged event for the window |
| OnStateChanged | Raises the StateChanged event for the window |
| OnStyleChanged | Allows you to check the style of the window |
| Show | Displays the window |
| ShowDialog | Displays a dialog box |

Table 9.3 lists the noteworthy events of the Window class:

## Table 9.3: Noteworthy Events of the Window Class

| Event | Description |
|---|---|
| Activated | Occurs when the window is activated, that is, when the window becomes the active window |
| Closed | Occurs just before the window is closed |
| Closing | Occurs before the window is closed but provides you the option to cancel the closing of the window |
| ContentRendered | Occurs after the content of the window is rendered |
| Deactivated | Occurs when the window is no longer an active window |
| LocationChanged | Occurs when the position of the window changes |
| StateChanged | Occurs when the state of the window changes |

As stated earlier, a standalone WPF application can have more than one window. However, there is only one main application window, which is its first window by default.

> NOTE
> Standalone WPF applications run with all the privileges of the current user.

## XAML Browser Applications

As the name suggests, XAML Browser Applications (XBAP, pronounced as x-bap) are Web server-hosted WPF applications that run in a Web browser. XBAPs consist of several pages, which the users can access and navigate through the browser. This is similar to the working of traditional Web sites. Unlike the standalone WPF applications, XBAPs are not installed on the users' computers. This implies that if the users are offline (disconnected from the Internet or the server on which the XBAP is hosted), they cannot access XBAP. Note that XBAPs can be accessed from the Internet Explorer and Firefox Web browsers. Another key difference between XBAPs and standalone WPF applications is that XBAPs have limited privileges while standalone WPF applications run with the privileges of the currently logged-in desktop user.

> NOTE
> You can access XBAPs, if .NET Framework is present on users' computers. When you compile an XBAP, it is compiled to an .xbap extension while a Windows application is compiled to an .exe extension.

## Project Template and Files of an XBAP

Visual Studio 2010 provides a project template for creating XBAPs. Perform the following steps to create an XBAP:

- 1. Click the Start → All Programs → Microsoft Visual Studio 2010 → Microsoft Visual Studio 2010 option. Visual Studio 2010 IDE opens.
