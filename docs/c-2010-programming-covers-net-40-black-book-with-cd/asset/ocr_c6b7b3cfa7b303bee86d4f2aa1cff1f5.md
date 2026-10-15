information for further processing. Some common examples of modal dialog boxes include dialog boxes for opening and saving files.

+   Modeless dialog box – Refers to a dialog box that does not prevent the users from working with other windows of the application. In other words, modeless dialog boxes do not affect the functioning of the application. Therefore, these dialog boxes are suitable to display information, such as the current page number.

In WPF 4.0, you can use both modal and modeless dialog boxes in standalone WPF applications. WPF provides various classes to create dialog boxes and use them in applications. Some of the classes include the MessageBox, OpenFileDialog, SaveFileDialog, and PrintDialog classes. The MessageBox class provides the functionality to work with message boxes, while the OpenFileDialog, SaveFileDialog, and PrintDialog classes allow you to perform some common operations, such as opening, saving, and printing files, respectively. Let’s discuss each of these classes one at a time starting with the MessageBox class.

# The MessageBox Class

The MessageBox class (in the PresentationFramework assembly in the System.Windows namespace) allows you to create message boxes that are the simplest modal dialog box available. Message boxes are used to display some information that can further be used to confirm a particular action or make decisions. The information appears as textual message along with an OK button. The MessageBox class has the Show() method that allows you to display a message box. When the message box appears, by default an OK button is also displayed. However, you can also display other buttons, such as the Cancel, Yes, and No buttons. You can use the MessageBoxButton enumeration to specify the buttons that you want to display in the message box. If you want to take some action based on the button that a user has clicked, then you can capture the result in an instance of the MessageBoxResult class. If you want to convey the readers whether the message is a warning or additional information, then you can display an icon on the message box by using the MessageBoxImage enumeration. The MessageBoxImage enumeration provides several predefined icons that can be used.

# The OpenFileDialog Class

The OpenFileDialog class (available in the PresentationFramework assembly in the Microsoft.Win32 namespace) allows the users to provide the name of one or more files that are to be opened. The inheritance hierarchy of the OpenFileDialog class in WPF 4.0 is as follows:

```
System.Object
  Microsoft.Win32.CommonDialog
    Microsoft.Win32.FileDialog
      Microsoft.Win32.OpenFileDialog
```

The OpenFileDialog class in WPF is almost the same as the OpenFileDialog class in Windows Forms. For instance, the OpenFileDialog class in WPF and Windows Forms have the ShowDialog() and OpenFile() methods, the FileName and Filter properties, and the FileOk event. However, the OpenFileDialog class in WPF has two additional methods, CheckPermissionToShowDialog() and OpenFiles(). The CheckPermissionToShowDialog() method allows you to check if the necessary permissions are present to display the dialog box and the OpenFiles() method allows you to specify multiple files by creating an array of read-only streams for each of the files.

# The SaveFileDialog Class

The SaveFileDialog class (available in the PresentationFramework assembly in the Microsoft.Win32 namespace) allows you to specify the name, location, and type with which you want to save a file. The inheritance hierarchy of this class is as follows:

```
System.Object
  Microsoft.Win32.CommonDialog
    Microsoft.Win32.FileDialog
      Microsoft.Win32.SaveFileDialog
```

The SaveFileDialog class in WPF is almost the same as the SaveFileDialog class in Windows Forms. For instance, the SaveFileDialog class in WPF and Windows Forms has the CheckFileExists, FileName, and InitialDirectory properties. However, the SaveFileDialog class in WPF has two additional properties, named SafeFileName and