```vb
Private Sub SummaryForm_FormClosing(ByVal sender As Object, _
    ByVal e As System.Windows.Forms.FormClosingEventArgs) _
    Handles Me.FormClosing
        ' Release the resources of this form.

        AnInstance = Nothing
End Sub
End Class
```

# AboutBox

If you use the AboutBox template, you don’t have to write any code at all.

# SplashScreen

If you use the Splash Screen template, add one event handler to hold the form on the screen for a few seconds.

```
```vb
Private Sub SplashScreen1_FormClosing(ByVal sender As Object, _
    ByVal e As System.Windows.Forms.FormClosingEventArgs) _
    Handles Me.FormClosing
        ' Hold the form on the screen for about 5 seconds before closing.

        System.Threading.Thread.Sleep(5000)
End Sub
```
```

# Summary

+   1. The .NET Framework contains the class libraries, the common language runtime, and ASP.NET.
+   2. Managed code is compiled to run in the common language runtime (CLR).
+   3. A portable executable (PE) file contains intermediate language (managed code) and metadata.
+   4. Metadata store information about the methods, classes, and types for the runtime.
+   5. The .NET Framework is composed of a set of classes stored in the class library. The classes are organized into a hierarchy of namespaces.
+   6. The CLR treats value types and reference types differently. Each value type variable has the value stored in the variable’s memory location and is always initialized. A reference type variable holds a pointer to an actual object and may be equal to Nothing if not assigned.
+   7. The compiler produces MSIL (Microsoft intermediate language), a platform-independent set of instructions.
+   8. An assembly is the smallest deployable unit of code, which contains one or more .exe or .dll files and a manifest that describes the assembly.
+   9. The AssemblyInfo.vb file holds attributes, which are tags that contain information about the assembly.
+   10. A Reference object connects Visual Basic to external components, either assemblies or COM objects.