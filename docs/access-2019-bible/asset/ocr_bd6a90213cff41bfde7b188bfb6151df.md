In this procedure, the `frmProgress` form is opened and assigned to a variable that allows access to the Max property and the UpdateProgress method. The Max property is set to `rs.RecordCount`, and the UpdateProgress method is called within the loop, passing the `iCnt` variable. Finally, the progress form is closed at the end of the procedure.

# Making the application easy to start

You shouldn’t expect users to locate the Access data file (ACCDB or MDB) or to choose File ▸ Open in Access to invoke the application. Pinning items to the Windows Start screen isn’t difficult. When properly implemented, a program icon creates the impression that the application exists as an entity separate from Access and endows it with a status equivalent to Word, Excel, or other task-oriented programs.

Creating a program icon isn’t difficult. Many freeware and shareware versions of icon editors are available online, enabling you to create entirely new icons. The Chapter31.accdb example database comes with its own program icon (Earth.ico) for you to experiment with. You designate the program icon in the Access startup options (see the “Application options” section earlier in this chapter) or by setting a program icon in File Explorer.

Follow these steps to establish a Windows shortcut for an Access database application:

+   1. In the Microsoft Office program folder (usually C:\Program Files\Microsoft Office\root\Office16), locate MSACCESS.EXE.
+   2. Right-click MSACCESS.EXE and select Create Shortcut.
+   3. Press F2 while the shortcut is highlighted and enter a new caption for the icon.
+   4. Right-click the icon and select Properties. The icon’s Properties dialog box appears.
+   5. Select the Shortcut tab and add a complete path reference to the application’s ACCDB or MDB file to the Target text box.

> CAUTION
> Be sure not to delete or alter the path to the Access executable file.

In Figure 31.14 the application database’s path is M:\Chapter31.accdb. Notice that the Target text box contains the path to the Access executable followed by the path to the ACCDB file.

> NOTE
> If the path to the database includes spaces, you need to put double quotes around the full path.