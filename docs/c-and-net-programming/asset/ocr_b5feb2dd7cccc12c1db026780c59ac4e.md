+   1. **Windows application** - A Windows Forms-based project including Windows CE .NET-specific controls. This is the most commonly used template because it generates Windows-based applications.
+   
+   2. **Class library** - Class libraries allow to package related components in a single file. They can be used to develop other applications or as a base for inheritance for other components. This project type is best suited for creating modules of code that will be reused with multiple applications.
+   
+   3. **Console application** - Used to create executables that will run within the console window. Best used for background and maintenance applications, which may or may not require user interaction. Unlike the Pocket PC, Windows CE natively supports console applications.
+   
+   4. **Empty project** - Defines a project with no predefined components, allowing to custom-build everything from the ground up.

# 28.1.8 .NET Compact Framework - Application Architecture

+   - The .NET compact framework application consists of below modules bundled in as a single application for various types of devices.

![](bbox=[0.1, 0.57, 0.95, 0.88])

+   - In addition to being abstracted from the native operating system services, the applications also inherit other advantages such as fault isolation, security, and better resource management, because they run within separate application domain hosts. Currently, the .NET Compact Framework supports Pocket PC and Windows CE .NET-based platforms.