The highest-level portion of the application is called `Testbed2DApp`; it is implemented in the files `Testbed2DApp.xaml` (the XAML file) and `Testbed2DApp.xaml.cs` (the associated C# file).

The XAML file (see Listing 4.1) declares that `Testbed2D` is an object of class `Application`, which means that it has certain properties, events, and methods pre-defined; we use almost none of these, with the exception of the `Startup` event handler, which we'll see in the C# file.^1

# *Listing 4.1: The code in Testbed2DApp.xaml.*

```
```xml
<Application x:Class="Testbed2D.Testbed2DApp"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    Startup="AppStartupUp">
    <Application.Resources />
</Application>
```
```

The code in Listing 4.1 simply declares an application and some information about where to find certain name resolutions (the `xmlns` lines) for this XML namespace. The key element, from our point of view, is the line `Startup="AppStartupUp"`, which says that the `Startup` event is to be handled by code that will be found in the `AppStartingUp` method of the `Testbed2D.xaml.cs` file. This is the equivalent of `main()` in a C++ or Java program.

The corresponding C# file is shown in Listing 4.2. The keyword `partial` tells us that part of the class's description is here, but part of it is elsewhere (in the XAML file). The `AppStartingUp` method has been defined to create a `Window` and to show it. The arguments to `AppStartingUp` are unused. The remaining event handlers, methods, etc., for the `Testbed2DApp` remain unchanged from the defaults inherited from the `Application` class.

# *Listing 4.2: The corresponding C# file, Testbed2DApp.xaml.cs.*

```
```csharp
using System;
using ...;

namespace Testbed2D
{
    public partial class Testbed2DApp : Application
    {
        void AppStartingUp(object sender, StartupEventArgs e)
        {
            Window mainWindow = new Window();
            mainWindow.Show();
        }
    }
}
```
```

So, if we run the `Testbed2DApp`, upon startup a `Window` will be created and shown.

This `Window` class is somewhat richer than the `Testbed2DApp` class: It corresponds to the main window of a conventional application and includes things like