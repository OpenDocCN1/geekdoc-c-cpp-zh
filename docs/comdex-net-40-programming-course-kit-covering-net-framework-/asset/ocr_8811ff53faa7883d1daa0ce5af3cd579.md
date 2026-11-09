![](bbox=[0.262, 0.136, 0.762, 0.406])

Fig.VB-5.3

You can notice in Fig.VB-5.3 that similar to Windows Forms applications, the design interface of the new WPF standalone application has a **Toolbox** with various tools, and a blank rectangular area, called *window*. You learn more about the design interface of WPF standalone application later in the chapter.

As already learned, when you create a WPF standalone application by using the **WPF Application** template, the application will create an application.xaml. MainWindow.xaml required for working with WPF applications are automatically added to the application. You can view these files in the **Solution Explorer** window, which can be opened by selecting **View→Solution Explorer** from the menu bar or pressing the **CTRL+ALT+L** keys on the keyboard (Fig.VB-5.4).

You can notice in Fig.VB-5.4 that two files, **Application.xaml** and **MainWindow.xaml**, are displayed in the **Solution Explorer** window by default. The **Application.xaml** node contains another file, **Application.xaml.vb**, which you can display by expanding this node. The **Application.xaml** and **Application.xaml.vb** files collectively represent the entire WPF application. The **Application.xaml** file is an XAML file, that is, a file written in XAML, and the **Application.xaml.vb** file is its code-behind file (in Visual Basic). You can use these files to specify application-level settings and logic. The **MainWindow.xaml** node also contains another file, **MainWindow.xaml.vb**, which you can display by expanding this node. The **MainWindow.xaml** and **MainWindow.xaml.vb** files correspond to the default UI of a WPF standalone application, which consists of a single blank window. The **MainWindow.xaml** file is an XAML file; whereas, the **MainWindow.xaml.vb** file is its code-behind file (in Visual Basic). These two files contain the settings and logic for the default window in a WPF standalone application.

> > A window in a WPF standalone application is an object of the Window class.

By default, the **Solution Explorer** window does not show all the files in the standalone application. You need to click the **Show All Files** button in the toolbar of the **Solution Explorer** window to view all the files included in the standalone application, (Fig.VB-5.4)

When you click the **Show All Files** button in the **Solution Explorer** window, all the files included in the standalone application become visible (Fig.VB-5.5). For example, files that were not visible by default appear under the **References**, **bin**, and **obj** nodes of the **Solution Explorer** window.