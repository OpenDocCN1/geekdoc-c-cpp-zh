namespace throughout the XAML document; it's what you use to instantiate an object from a class in that namespace.

For instance, if you want to add the namespace `MyTemplates.DataTemplates` from the assembly `MyTemplates.dll`, you could define the namespace as

```
`xmlns:myDTs="clr-namespace:MyTemplates.DataTemplates;assembly=MyTemplates.dll"`
```

You are then able to instantiate an object from the MyTemplates.DataTemplates namespace as follows:

```
`<myDTs:MyClass></myDTs:MyClass>`
```

# ### Declaring an application-scoped resource

To demonstrate the creation and use of a global application-scoped resource, in this section, you create a resource that holds a string used in our application. An application-scoped resource is available to all Windows and user controls defined in the project. Follow these steps:

+   1. Add the `System` namespace located in the `mscorlib.dll` assembly. This is where the `String` class is located.
+   2. To do this, add the following namespace to the `App.xaml` root element:
+      `xmlns:sys="clr-namespace:System;assembly=mscorlib"`
+      The `String` class is now available for use throughout the `App.xaml` document.
+   3. Create the resource between the `Application.Resource` tags, add the following `String` class element:
+      `<sys:String x:Key="Purpose">Hello WPF World!</sys:String>`
+      This element instantiates an object of type `String`, initialized to the value Hello WPF World!, and keyed off of the key `Purpose`. This resource is now available throughout the `MyFirstWPFApplication` application by requesting the resource "Purpose" (see Listing 1-2).

# **Listing 1-2: Updated App.xaml with Resource and System Namespace Defined**

```
```xml
<Application x:Class="MyFirstWPFApplication.App"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    xmlns:sys="clr-namespace:System;assembly=mscorlib"
    StartupUri="MainWindow.xaml">
    <Application.Resources>
        <sys:String x:Key="Purpose">Hello WPF World!</sys:String>
    </Application.Resources>
</Application>
```
```