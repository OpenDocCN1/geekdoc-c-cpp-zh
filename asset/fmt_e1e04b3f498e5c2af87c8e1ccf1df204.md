
The `OpenFileDialog` class in WPF is almost the same as the `OpenFileDialog` class in Windows Forms. For instance, the `OpenFileDialog` class in WPF and Windows Forms have the `ShowDialog()` and `OpenFile()` methods, the `FileName` and `Filter` properties, and the `FileOk` event. However, the `OpenFileDialog` class in WPF has two additional methods, `CheckPermissionToShowDialog()` and `OpenFiles()`. The `CheckPermissionToShowDialog()` method allows you to check if the necessary permissions are present to display the dialog box and the `OpenFiles()` method allows you to specify multiple files by creating an array of read-only streams for each of the files.

## The SaveFileDialog Class

The `SaveFileDialog` class (available in the `PresentationFramework` assembly in the `Microsoft.Win32` namespace) allows you to specify the name, location, and type with which you want to save a file. The inheritance hierarchy of this class is as follows:

```
System.Object
  Microsoft.Win32.CommonDialog
    Microsoft.Win32.FileDialog
      Microsoft.Win32.SaveFileDialog
```

The `SaveFileDialog` class in WPF is almost the same as the `SaveFileDialog` class in Windows Forms. For instance, the `SaveFileDialog` class in WPF and Windows Forms has the `CheckFileExists`, `FileName`, and `InitialDirectory` properties. However, the `SaveFileDialog` class in WPF has two additional properties, named `SafeFileName` and `SafeFileNames`. The `SafeFileName` property retrieves the name of the selected file, while the `SafeFileNames` property retrieves an array containing a safe file name for the individual files.

## The PrintDialog Class

The `PrintDialog` class (available in the `PresentationFramework` assembly in the `System.Windows.Controls` namespace) allows you to specify and configure the printer. It also allows you to specify various settings and options related to the printing process. The inheritance hierarchy of the `PrintDialog` class is as follows:

```
System.Object
System.Windows.Controls.PrintDialog
```

The `PrintDialog` class in WPF is similar to the `PrintDialog` class in Windows Forms. However, there are certain differences due to some additional properties and methods in the `PrintDialog` class of WPF. Table 9.15 lists some of the noteworthy properties of the `PrintDialog` class in WPF:

| Table 9.15: Noteworthy Properties of the PrintDialog Class |
| Property | Description |
| MaxPage | Sets or retrieves the maximum page number. |
| MinPage | Sets or retrieves the minimum page number. |
| PageRange | Sets or retrieves the range of pages that is to be printed. This property is available when the PageRangeSelection property is set to UserPages. |
| PageRangeSelection | Sets or retrieves the range of pages for printing. |
| PrintableAreaHeight | Retrieves the height of the printable portion on the page. |
| PrintableAreaWidth | Retrieves the width of the printable portion on the page. |
| PrintQueue | Sets or retrieves a PrintQueue object that manages the printers and print jobs. |
| PrintTicket | Sets or retrieves a PrintTicket object that allows you to specify the print job settings. |
| UserPageRangeEnabled | Specifies whether users of the Print dialog box can set the page range. |

Table 9.16 lists the noteworthy methods of the `PrintDialog` class:

| Table 9.16: Noteworthy Methods of the PrintDialog class |
| Method | Description |
| PrintDocument | Allows you to print an object with multiple pages through the PrintQueue object. |
| PrintVisual | Allows you to print non-textual visual content, that is, a Visual object through the PrintQueue object. |

Let’s now move on to learn how WPF applications are compiled and executed.

## Compiling and Running WPF 4.0 applications

After creating WPF 4.0 application, you can compile and run it. The compilation of WPF applications involves the compilation of the XAML and .NET language codes (`C#` code in the code-behind file). First, the XAML code is built or compiled using the XAML compiler into Binary Application Markup Language (`BAML`) files. Binary XAML files (`BAML` files) have the `.baml` extension and are embedded into the .NET assemblies. When the WPF application executes, this `BAML` file is used to create the visual tree that is used to render the UI elements in the WPF application.

You can build or compile WPF 4.0 applications in Visual Studio 2010 by selecting the `Build→Build Solution` option from the menu bar in the Visual Studio 2010 IDE. The XAML compiler then creates the `.baml` file and stores it in the `<WPFApplication>\<WPFApplicationProject>\obj\x86\Debug` folder. The compiler also creates another file called the generated file. The generated file is identified by the `.g.cs` (for `C#`) extension and created for the application and root element. For standalone WPF applications, there are at least two generated files, `App.g.cs` and `MainWindow.g.cs`. Similarly, `App.g.cs` and `Page1.g.cs` are the files that are generated for XBAPs. The generated files contain a partial class that defines the code to extract and load the `.baml` file from the assembly during run time and fields that correspond to the WPF controls used in the application. Listing 9.8 shows the content of the `MainWindow.g.cs` file of a standalone WPF application that has the `Button` and `Radio Button` elements:

### Listing 9.8: Displaying the Contents of a MainWindow.g.cs File

```
#pragma checksum "..\..\..\MainWindow.xaml" "{406ea660-64cf-4c82-b6f0-42d48172a799}"
"5F47F9792AEC132C418A12238B3F9902"
//------------------------------------------------------------------------------
// <auto-generated>
//     This code was generated by a tool.
//     Runtime Version:4.0.30319.1
//
//     Changes to this file may cause incorrect behavior and will be lost if
//     the code is regenerated.
// </auto-generated>
//------------------------------------------------------------------------------
using System;
using System.Diagnostics;
using System.Windows;
using System.Windows.Automation;
using System.Windows.Controls;
using System.Windows.Controls.Primitives;
using System.Windows.Data;
using System.Windows.Documents;
using System.Windows.Ink;
using System.Windows.Input;
using System.Windows.Markup;
using System.Windows.Media;
using System.Windows.Media.Animation;
using System.Windows.Media.Effects;
using System.Windows.Media.Imaging;
using System.Windows.Media.Media3D;
using System.Windows.Media.TextFormatting;
using System.Windows.Navigation;
using System.Windows.Shapes;
using System.Windows.Shell;
namespace wpfApplication1 {
    /// <summary>
    /// MainWindow
    /// </summary>
    [System.CodeDom.Compiler.GeneratedCodeAttribute("PresentationBuildTasks", "4.0.0.0")]
    public partial class MainWindow : System.Windows.Window, System.Windows.Markup.IComponentConnector {
        #line 14 "..\..\..\MainWindow.xaml"
        [System.Diagnostics.CodeAnalysis.SuppressMessageAttribute("Microsoft.Performance", "CA1823:AvoidUnusedPrivateFields")]
        internal System.Windows.Controls.Button button1;
        #line default
        #line hidden
        #line 15 "..\..\..\MainWindow.xaml"
        [System.Diagnostics.CodeAnalysis.SuppressMessageAttribute("Microsoft.Performance", "CA1823:AvoidUnusedPrivateFields")]
        internal System.Windows.Controls.RadioButton radioButton1;
        #line default
        #line hidden
        private bool _contentLoaded;
        /// <summary>
        /// InitializeComponent
        /// </summary>
        [System.Diagnostics.DebuggerNonUserCodeAttribute()]
        public void InitializeComponent() {
            if (_contentLoaded) {
                return;
```

}
_contentLoaded = true;
System.Uri resourceLocator = new
    System.Uri("/WpfApplication1;component/mainwindow.xaml",
    System.UriKind.Relative);
#line 1 "..\..\..\MainWindow.xaml"
System.Windows.Application.LoadComponent(this, resourceLocator);
#line default
#line hidden
}
[System.Diagnostics.DebuggerNonUserCodeAttribute()]
[System.ComponentModel.EditorBrowsableAttribute(System.ComponentModel.EditorBrowsableState.Never)]
```
