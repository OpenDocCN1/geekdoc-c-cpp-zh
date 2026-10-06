
```fsharp
let b = x - x / 10 * 10
? (a*2* b)
```

```fsharp
let data = [-100..100]
let resultData = data | List.filter (7)
```

```fsharp
// test data
let oracle =
    data
    | List.filter (fun n -> n % 7 = 0)
let c = resultData = oracle
```

Note This sample shows how to use a special character in the function name. Except for requiring that the active pattern name be started with an uppercase letter, F# does not impose any restrictions on names. You can even use Unicode characters in a function name.
You can use F# Interface (FSI) to print out lists using Alt+number key in the keyboard to type in the character, and FSI will figure out the characters. A sample is shown here. The first character is Alt + 900, and the last is Alt + 980. If your system does not have a keyboard, you can use the other system as Microsoft Word to generate these characters.

```fsharp
> ['à','...'];
val it : char list = [
['à'; 'á'; 'â'; 'ä'; 'è'; 'ë'; 'í'; 'î'; 'ï'; 'ò'; 'ó'; 'ö'; 'õ'; 'ù'];
['A'; 'Á'; 'Ã'; 'Ä'; 'E'; 'Ê'; 'Ë'; 'Í'; 'Î'; 'Ï'; 'Ò'; 'Ó'; 'Ö'; 'Õ'; 'Ú'];
['C'; 'Ç'; 'Œ'; 'É'; 'E'; 'Ê'; 'Ë'; 'Í'; 'Î'; 'Ï'; 'Ò'; 'Ó'; 'Ö'; 'Õ'; 'Ú'];
['D'; 'Ð'; 'E'; 'É'; 'ê'; 'ë'; 'í'; 'î'; 'ï'; 'ò'; 'ó'; 'ö'; 'õ'; 'ù'];
['G'; 'Ğ'; 'Ĝ'; 'H'; 'Ħ'; 'í'; 'î'; 'ï'; 'ò'; 'ó'; 'ö'; 'õ'; 'ù'];
['I'; ' ''; ''; 'í'; 'î'; 'ï'; 'ñ'; 'ò'; 'ó'; 'ö'; 'õ'; 'ù'; 'ú'; 'ý'; 'ÿ'];
['L'; 'Ł'; 'Ĺ'; 'ļ'; 'ñ'; 'ò'; 'ó'; 'ö'; 'õ'; 'ù'; 'ú'; 'ý'; 'ÿ'];
['N'; 'Ñ'; 'ń'; 'ò'; 'ó'; 'ö'; 'õ'; 'ù'; 'ú'; 'ý'; 'ÿ']; ... ]
```

# Developing the WinRT Application

In Visual Studio 2012, F# is shipped with a new template to call the F# Portable Library. This template is used for developing the WinRT application. When developing a WinRT application, you can use an F# portable library to host the business logic. C# can provide a UI for the portable library.

The portable library is the intersection of .NET frameworks: Silverlight, the desktop, and WinRT. Because the portable library is the subset of these .NET frameworks, moving an application from a desktop environment to a portable library does not work in some cases. For example, System.IO.File is not present in the portable library because the Silverlight .NET framework does not support System.IO.File.

If you want to develop business logic for WinRT applications, F# portable library is a good choice. The F# portable library is designed to be executed within Windows Store applications, Silverlight applications, and desktop applications. You will now create a Windows Store application that will serve as the UI controller for the examples in the rest of this chapter.

When creating a new project, you can expand the C# node and select the Windows Store node in Visual Studio 2012 on Windows 8. Blank App is the template you are going to use, as shown in Figure 7-6.

![](img/63aaf94e22830ab98ce16c5946be8ef6_406_0.png)

> The initial release of F# 3.0 with Visual Studio 2012 did not include some important settings, which caused the Windows 8 verification process to fail for Windows 8 applications that used F#. This Windows 8 verification bug has been fixed in the Visual Studio Update. If installing the Visual Studio Update is not an option, you can resolve this by editing the csp file for the project and adding the following at the end of the first PropertyGroup:

```xml
<PropertyGroup Condition="$(Configuration)|$(Platform) == 'Release|AnyCPU'">
    <OtherFlags>-staticlink:FSharp.Core</OtherFlags>
</PropertyGroup>
```

# New Project

- Recent
- Installed
- Visual C#
- Light
- Other Languages
- Visual Basic
- Windows Store
- Web
- Office
- Reporting
- SharePoint
- Unity

**Sort By:** Default

| Visual C# | Visual C# |
|---|---|
| Blank App (XAML) | A simple project for a Windows Store app that uses predefined controls or layouts. |
| Split App (XAML) | |
| Class Library (Windows Store app) | |
| Runtime Component | |
| Unit Test Library (Windows Store... | |

- Online
- Name: WinUI
- Location: C:\Projects\
- Solution name: WinUI

**FIGURE 7-6** Creating a Windows Store app (XAML) project

An example of the generated solution is shown in Figure 7-7.

![](img/63aaf94e22830ab98ce16c5946be8ef6_407.png)

**FIGURE 7-7** Windows 8 application generated from the Blank template

From the properties page, the F# portable library can be configured to target WinRT, .NET 4.5, and Silverlight 5. See Figure 7-8.

| Configuration: N/A | Platform: N/A |
|---|---|
| Build | |
| Build Events: WinUI | |
| Debug | |
| Reference Paths: | |
| Target Framework: .NET Portable Subset (Windows Store apps) | Output type: Class Library |
| .NET Portable Subset (Windows Store apps, .NET 4.5, Silverlight 5) | |
| Resources: | |
| Specify how application resources will be managed: | |
| Resource File: |

**FIGURE 7-8** Portable library project page

PART III Real-World Applications

You can add a text block to the main form, as shown in Listing 7-4.

# LISTING 7-4 XAML code in the main form

```xml
<Page
  x:Class="WinUI.MainPage"
  xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
  xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
  xmlns:local="http://schemas.microsoft.com/expression/blend/2008"
  xmlns:mc="http://schemas.microsoft.com/expression/xmlformats/markup-compatibility/2006"
  mc:Ignorable="d">

  <Grid Background="StaticResource ApplicationPageThemeBrush">
    <TextBlock x:Name="result_box" Text="Result"/>
  </Grid>
</Page>
```

The F# portable library project can now be created in the solution, as shown in Figure 7-9.

![](img/63aaf94e22830ab98ce16c5946be8ef6_408_0.png)

**FIGURE 7-9** Creating an F# portable library in the Win8UI solution

The new solution structure with the F# Portable Class Library project is shown in Figure 7-10.

# Solution Explorer

![](img/63aaf94e22830ab98ce16c5946be8ef6_409_0.png)

**FIGURE 7-10** Solution structure with the F# Portable Class Library project and Win8UI project

For brevity, I am not going through a complete MVVM implementation. Instead, I will provide just enough of an implementation to enable data binding. The first modification that is required to add the *Result* member to *Class1* in the PortableLibrary1.fs file, as shown in Listing 7-5.

**LISTING 7-5** Code change in the PortableLibrary1.fs

```fsharp
namespace FSharpPortable

type Class1() =
    member this.Result = "F#"
```

The UI project can now be enhanced to bind to our F# portable library. In this step, *DataContext* is set to *Class1* and the UI XAML code is changed to bind to the *Result* property, as shown in Listing 7-6.

**LISTING 7-6** Code change in the Win8UI project to enable data binding

```xml
XAML code change
<Page
    x:Class="Win8UI. MainPage"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    xmlns:local="http://schemas.microsoft.com/expression/blend"
    xmlns:d="http://schemas.openxmlformats.org/markup-compatibility/2006"
    mc:Ignorable="d">

    <Grid Background="{StaticResource ApplicationPageBackgroundThemeBrush}">
        <TextBlock x:Name="result_box" Text="{Binding Result}" />
    </Grid>
</Page>
```

```csharp
C# code to set DataContext
using System;
using System.Collections.Generic;
using System.IO;
```
