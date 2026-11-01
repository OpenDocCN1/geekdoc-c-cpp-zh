+   - Translate the content.
+   - Create satellite assemblies for every language.

These steps are described in the following sections.

# Create Satellite Assemblies

When compiling a WPF application, the XAML code is compiled to a binary format, BAML, that is stored into an assembly. To move the BAML code from the main assembly to a separate satellite assembly, you can change the .csproj build file and add a <UICulture> element as shown as a child to the <PropertyGroup> element. The culture, here en-US, defines the default culture of the project. Building the project with this build setting creates a subdirectory en-US and creates a satellite assembly containing BAML code for the default language.

```
```xml
<UICulture>en-US</UICulture>
```
*code snippet WPFApplicationUsingXAML.Dictionaries/WPFApplicationUsingXAML.Dictionaries.csproj*
```

> > The easiest way to modify the project settings that are not available from the UI is to unload the project by selecting the project in the Solution Explorer and select Unload Project from the context menu, and next click Edit project-file from the context menu. After the project file is changed, the project can be loaded again.

Separating the BAML into a satellite assembly, you should also apply the NeutralResourcesLanguage attribute and supply the resource fallback location to a satellite assembly. If you decide to keep BAML in the main assembly (by not defining the <UICulture> to the .csproj file), the UltimateResourceFallbackLocation should be set to MainAssembly.

```
```csharp
[assembly: NeutralResourcesLanguage("en-US")]
[assembly: UltimateResourceFallbackLocation.Satellite]
```
*code snippet WPFApplicationUsingXAML.Dictionaries/AssemblyInfo.cs*
```

# Add a Resource Dictionary

For code-behind content that needs to be localized, a resource dictionary can be added. Using XAML, you can define resources within the <ResourceDictionary> element as shown. With Visual Studio, you can create a new resource dictionary by adding a new resource dictionary item and defining the filename. In the example here, the resource dictionary contains one string item. To get access to the String type from the System namespace, an XML namespace alias needs to be defined. Here, the alias system is set to the clr-namespace System in the assembly mscorlib. The string that is defined can be accessed with the key message1. This resource dictionary is defined in the file LocalizedStrings.xaml.

```
```xml
<ResourceDictionary
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    xmlns:system="clr-namespace:System;assembly=mscorlib">
    <system:String x:Key="Message1">English Message</system:String>
</ResourceDictionary>
```
*code snippet WPFApplicationUsingXAML.Dictionaries/LocalizationStrings.xaml*
```

To have the resource dictionary available with the application, it must be added to the resources. If the resource dictionary is required only within a window or just within a specific WPF element, it can be added to the resources collection of the specific window or WPF element. If the same resource dictionary is needed by multiple windows, it can be added to the file App.xaml within the <Application> element, and thus