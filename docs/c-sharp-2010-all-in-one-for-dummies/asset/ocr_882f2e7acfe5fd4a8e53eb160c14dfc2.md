The no-PIA feature allows you to continue to use PIAs at design time without having them around at runtime. Instead, the C# 4.0 compiler bakes the small part of the PIA that a program actually uses directly into its assembly. The PIA doesn't have to be loaded at runtime.

To see how this works, try these steps in both Visual Studio 2010 and Visual Studio 2008 (if you have it):

+   1. Create a new console application by choosing File→New→Project and picking C#→Console application. Name your project PIAs.
+   2. After the project loads, right-click on References.
+   3. Click Add Reference.
+   4. Select Microsoft.Office.Interop.Excel, version 12, if you have it. Otherwise, use the latest version you have loaded.
+   5. Click OK.
+   6. Add using Microsoft.Office.Interop.Excel; to the header.
+   7. Change the Main procedure to the following (just enough to get Excel rolling):
+   8. Right-click on the Solution and select Add Project.
+   9. Add a new Setup project.
+   10. Right-click on the Setup project and choose Add→Project Output.
+   11. Select Primary Output.
+   12. Click OK.

```
static void Main(string[] args)
{
    Microsoft.Office.Interop.Excel.Application
    xl = new Application();
    xl.Quit();
}
```

The setup project will automatically determine what to deploy with the application. In Visual Studio 2008, with C# 3.0, it will deploy the primary Interop assemblies, as shown in Figure 3-1.

In Visual Studio 2010, the setup doesn't deploy the PIAs. The specific parts being used are compiled right into the EXE for the application. This is demonstrated in Figure 3-2.