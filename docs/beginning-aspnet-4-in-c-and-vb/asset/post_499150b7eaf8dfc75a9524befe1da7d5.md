
- Translate the content.
- Create satellite assemblies for every language.

These steps are described in the following sections.

## Create Satellite Assemblies

When compiling a WPF application, the XAML code is compiled to a binary format, BAML, that is stored into an assembly. To move the BAML code from the main assembly to a separate satellite assembly, you can change the .csproj build file and add a <UICulture> element as shown as a child to the <PropertyGroup> element. The culture, here en-US, defines the default culture of the project. Building the project with this build setting creates a subdirectory en-US and creates a satellite assembly containing BAML code for the default language.

```xml
<UICulture>en-US</UICulture>
```
*code snippet WPFApplicationUsingXAML.Dictionaries/WPFApplicationUsingXAML.Dictionaries.csproj*

> The easiest way to modify the project settings that are not available from the UI is to unload the project by selecting the project in the Solution Explorer and select Unload Project from the context menu, and next click Edit project-file from the context menu. After the project file is changed, the project can be loaded again.

Separating the BAML into a satellite assembly, you should also apply the NeutralResourcesLanguage attribute and supply the resource fallback location to a satellite assembly. If you decide to keep BAML in the main assembly (by not defining the <UICulture> to the .csproj file), the UltimateResourceFallbackLocation should be set to MainAssembly.

```csharp
[assembly: NeutralResourcesLanguage("en-US")]
[assembly: UltimateResourceFallbackLocation.Satellite]
```
*code snippet WPFApplicationUsingXAML.Dictionaries/AssemblyInfo.cs*

## Add a Resource Dictionary

For code-behind content that needs to be localized, a resource dictionary can be added. Using XAML, you can define resources within the <ResourceDictionary> element as shown. With Visual Studio, you can create a new resource dictionary by adding a new resource dictionary item and defining the filename. In the example here, the resource dictionary contains one string item. To get access to the String type from the System namespace, an XML namespace alias needs to be defined. Here, the alias system is set to the clr-namespace System in the assembly mscorlib. The string that is defined can be accessed with the key message1. This resource dictionary is defined in the file LocalizationStrings.xaml.

```xml
<ResourceDictionary
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    xmlns:system="clr-namespace:System;assembly=mscorlib">
    <system:String x:Key="Message1">English Message</system:String>
</ResourceDictionary>
```
*code snippet WPFApplicationUsingXAML.Dictionaries/LocalizationStrings.xaml*

To have the resource dictionary available with the application, it must be added to the resources. If the resource dictionary is required only within a window or just within a specific WPF element, it can be added to the resources collection of the specific window or WPF element. If the same resource dictionary is needed by multiple windows, it can be added to the file App.xaml within the <Application> element, and thus be available to the complete application. Here, the resource dictionary is added within the resources of the main window:

```xml
<Window.Resources>
  <ResourceDictionary>
    <ResourceDictionary.MergedDictionaries>
      <ResourceDictionary Source="LocalizationStrings.xaml" />
    </ResourceDictionary.MergedDictionaries>
  </ResourceDictionary>
</Window.Resources>
```
*code snippet WPFApplicationUsingXAML.Dictionaries/MainWindow.xaml*

To use the XAML resource dictionary from code behind, you can use the indexer of the Resources property, the FindResource() method or the TryFindResource() method. Because the resource is defined with the window, the indexer of the Resources property of the Window class can be used to access the resource. FindResource() does a hierarchical search for a resource. If you use the FindResource() method of the Button, and if it is not found with the Button resources, then resources are searched in the Grid. If the resource is not there, a lookup to the Window resources is done before the Application resources are consulted.

```csharp
private void Button_Click(object sender, RoutedEventArgs e)
{
    MessageBox.Show(this.Resources["Message1"] as string);
    MessageBox.Show(this.FindResource("Message1") as string);
}
```
*code snippet WPFApplicationUsingXAML.Dictionaries/MainWindow.xaml.cs*

## Uid Attributes for Localization

With the custom resource dictionary file, the text from the code that should be localized can be referenced. For localizing XAML code with WPF elements, the x:Uid attribute is used as a unique identifier for the elements that need localization. You don't have to apply this attribute manually to the XAML content; instead, you can use the msbuild command with this option:

```
msbuild /t:updateuid
```

When you call this command in the directory where the project file is located, the XAML files of the project are modified to add an x:Uid attribute with a unique identifier to every element. If the control already has a Name or x:Name attribute applied, the x:Uid has the same value; otherwise, a new value is generated. The same XAML that was shown before now has the new attributes applied:

```xml
<Window x:Uid="Window_1"
  x:Class="WPFApplicationUsingXAML.Dictionaries.MainWindow"
  xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
  xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
  Title="Main Window" Height="240" Width="500">
  <Window.Resources>
    <ResourceDictionary x:Uid="ResourceDictionary_1">
      <ResourceDictionary.MergedDictionaries>
        <ResourceDictionary x:Uid="ResourceDictionary_2" Source="LocalizationStrings.xaml" />
      </ResourceDictionary.MergedDictionaries>
    </ResourceDictionary>
  </Window.Resources>
  <Grid x:Uid="Grid_1">
    <Button x:Uid="button1" Name="button1" Margin="30,30,30,20" Click="Button_Click" Content="English Button" />
  </Grid>
</Window>
```

If you change the XAML file after x:Uid attributes have been added, you can verify correctness of the x:Uid attributes with the option /t:checkuid.

Now you can compile the project to create BAML code containing the x:Uid attributes and use a tool to extract this information.

## LocBaml Tool for Localization

Compiling the project creates a satellite assembly containing the BAML code. From this satellite assembly, you can extract the content that needs to be localized with classes from the System.Windows.Markup.Localizer namespace. With the Windows SDK, you will find the sample program LocBaml. This program can be used to extract localization content from BAML. You need to copy the executable, the satellite assembly with the default content, and LocBaml.exe to one directory and start the sample program to produce a .csv file with the localization content:

```
LocBaml /parse WPFApplicationUsingXAML.Dictionaries.resources.dll /out:trans.csv
```

> To use the LocBaml with a WPF application that is built with .NET 4, the tool also must be built with .NET 4 or a newer version. If you have an old version of the LocBaml tool that was built with .NET 2.0, it cannot load the .NET 4 assemblies. The Windows SDK contains the source of the tool, so you can rebuild it with the newest version of .NET.

You can use Microsoft Excel to open the .csv file and translate its content. An extract from the .csv file that lists the content of the button and the message from the resource dictionary is shown here:

```
WPFandXAMLResources.g.en-US.resources:localizationstrings.baml,
system:String_i:System.String.Content,None,True,True,, English Message
WPFandXAMLResources.g.en-US.resources:window1.baml,
button1:System.Windows.Controls.ContentControl.Content,Button,True,True,, English Button
```

This file contains these fields:

- Name of the BAML
- The identifier of the resource
- The category of the resource that gives the type of the content
- A Boolean value if the resource is visible for translation (readable)
- A Boolean value if the resource can be modified for the translation (modifiable)
- Localization comments
- The value of the resource

After localization of the resource, you can create a new directory for the new language (for example, de for German). The directory structure follows the same convention that was shown earlier in this chapter with satellite assemblies. With the LocBaml tool, you can create satellite assemblies with the translated content:

```
LocBaml /generate WPFandXAMLResources.resources.dll /trans:trans_de.csv /out:./de /cul:de-DE
```

Now the same rules for setting the culture of the thread and finding satellite assemblies that were shown with Windows Forms applications apply here.

As you've seen, it's quite a chore to do the localization with XAML dictionaries. This is one of the disadvantages. Luckily it's not necessary to do this day by day. What are the advantages?
