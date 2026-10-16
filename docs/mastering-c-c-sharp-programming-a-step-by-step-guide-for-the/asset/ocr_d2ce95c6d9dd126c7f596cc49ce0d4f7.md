In the Project directory, there are several files used to create the compiled program for the application. For basic projects, like SimpleForm, the files that are generated are:

+   - **App.ico -** This is the default icon for your application.
+   - **AssemblyInfo.cs –** This a C# source file that has the attribute declarations for targeting the project-generated assembly.
+   - **Form1.cs –** This the main project source file.
+   - **Form1.resx -** T\this is an XML file that is used for storing resource information that goes with Form1.cs.
+   - **SimpleForm.csproj –** This is the main C# project file.
+   - **SimpleForm.csproj.user –** This is a C# project file where you can find settings that are user-specific.
+   - **SimpleForm.sln -** This is the main C# project solution file.
+   - **SimpleForm.suo -** This is a C# solution file that has the information specific to users.

Out of all of these files, only two of them contain any source code – Form1.cs and AssemblyInfo.cs. The AssemblyInfo file will only contain assembly attributes that are used to define the characteristics for the assembly that is compiled and Form1.cs is where the bulk of the source code for the new project is found. When you open a source file that will implement a form, you will see the form displayed, at first, in design mode.

Press on F7 or right-click on the form and select View Code to see the source code for the form. Both ways will show the source code in a format so you can edit the code while, on another tab, C# .NET will keep the form in design mode open. Below is the standard contents of Form1.cs:

```
using System;
using System.Drawing;
using System.Collections;
using System.ComponentModel;
using System.Windows.Forms;
```