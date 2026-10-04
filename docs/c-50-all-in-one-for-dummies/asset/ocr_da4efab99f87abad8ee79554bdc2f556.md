+   3. In the Installed Templates region under the Visual C# section in the tree, click the Windows item.
4. Select WPF Application from the list box of templates located in the center of the window.
5. In the Name text box, enter MyFirstWPFApplication.
   This also sets the name of the solution to the same value, which is okay (see Figure 1-3).
6. Click OK.

Visual Studio now does its thing, creating the solution structure of the application. By default, as shown in Figure 1-4, the WPF Application template creates two XAML files along with their respective code-behind files: App.xaml (App.xaml.cs) and MainWindow.xaml (MainWindow.xaml.cs).

App.xaml represents the entry-point of the application. This is where application-wide (globally scoped) resources and the startup window are defined (see Listing 1-1).

Resources are a keyed collection of reusable objects. Resources can be created and retrieved using both XAML and C#. Resources can be anything — data templates, arrays of strings, or brushes used to color the background of text boxes. Resources are also scoped, meaning they can be available to the entire Application (global), to the Window, to the User Control, or even to only a specific control.

![](bbox=[0.25, 0.6, 0.83, 0.92])

![](bbox=[0.14, 0.47, 0.23, 0.54])