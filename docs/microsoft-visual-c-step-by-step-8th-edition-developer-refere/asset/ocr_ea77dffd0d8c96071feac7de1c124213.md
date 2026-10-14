```
canvas.Children.Remove(this.shape);
}
else
{
    this.shape = new Ellipse();
}

base.Draw(canvas);
}
```

9. On the Debug menu, click Start Debugging. When the Drawing Pad window opens, verify that Square objects appear when you left-click in the window and Circle objects appear when you right-click in the window. The application should behave the same as before.

10. Return to Visual Studio and stop debugging.

# Compatibility with the Windows Runtime revisited

Chapter 9, “Creating value types with enumerations and structures,” describes how the Windows platform from Windows 8 onward implements the Windows Runtime (WinRT) as a layer on top of the native Windows APIs, providing a simplified programming interface for developers building unmanaged applications. (An unmanaged application is an application that does not run by using the .NET Framework; you build them by using a language such as C++ rather than C#). Managed applications use the common language runtime (CLR) to run .NET Framework applications. The .NET Framework provides an extensive set of libraries and features. On Windows 7 and earlier versions, the CLR implements these features by using the native Windows APIs. If you are building desktop or enterprise applications and services on Windows 10, this same feature set is still available (although the .NET Framework itself has been upgraded to version 4.6), and any C# applications that work on Windows 7 should run unchanged on Windows 10.

On Windows 10, UWP apps always run by using WinRT. This means that if you are building UWP apps by using a managed language such as C#, the CLR actually invokes WinRT rather than the native Windows APIs. Microsoft has provided a mapping layer between the CLR and WinRT that can transparently translate requests to create objects and invoke methods that are made to the .NET Framework into the equivalent object requests and method calls in WinRT. For example, when you create a .NET Framework Int32 value (an int in C#), this code is translated to create a value using the equivalent WinRT data type. However, although the CLR and WinRT have a large amount of overlapping functionality, not all the features of the .NET Framework 4.6 have corresponding features in