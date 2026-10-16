create XAML code or write XAML code by hand. Visual Studio contains designers to write XAML code for WPF, Silverlight, WF, or Universal Windows apps. Other tools are also available to create XAML, such as Blend for Visual Studio 2015. Whereas Visual Studio is best for writing source code, Blend is best for creating styles, templates, and animations. With Visual Studio 2013, Blend and Visual Studio started to share the same XAML designer. Blend 2015 was rewritten to share the same shell with Visual Studio. As a Visual Studio user, you’ll immediately feel at home using Blend 2015.

Let’s get into XAML. With WPF applications, an XAML element maps to a .NET class, but that’s not a strict requirement for XAML. With Silverlight 1.0, .NET was not available with the plug-in and the XAML code was interpreted and could be accessed programmatically with JavaScript. This changed with Silverlight 2.0, in which a smaller version of the .NET Framework is part of the Silverlight plug-in. With Silverlight or WPF, every XAML element maps to a .NET class; with Windows Apps every XAML element maps to a Windows Runtime type.

What happens with XAML code on a build process? To compile a WPF project, MSBuild tasks are defined in the assembly PresentationBuildTasks named MarkupCompilePass1 and MarkupCompilePass2. These MSBuild tasks create a binary representation of the markup code named BAML (Binary Application Markup Language) that is added to the .NET resources of an assembly. During runtime, the binary representation is used.

# Mapping Elements to Classes with WPF

As mentioned earlier, usually an XAML element maps to a .NET or a Windows Runtime class. In this section you begin by creating a Button object inside a Window programmatically with a C# console project. To compile the following code, wherein a Button object is instantiated with the Content property set to a string, you define a Window with Title and Content properties set, and you need to reference the assemblies PresentationFramework, PresentationCore, WindowsBase, and System.Xaml (code file CodeIntroWPF/Program.cs).

```
using System;
using System.Windows;
using System.Windows.Controls;

namespace CodeIntroWPF
{
    class Program
    {
        [STAThread]
        static void Main()
        {
            var b = new Button
            {
                Content ="Click Me!"
            };
            b.Click += (sender, e) =>
            {
```