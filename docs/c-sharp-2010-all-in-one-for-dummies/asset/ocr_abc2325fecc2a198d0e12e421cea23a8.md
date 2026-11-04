![](bbox=[0.14, 0.13, 0.25, 0.22])

You are not expected to come up with things like the CheckPath off the top of your head. (The path is what describes how the check mark is drawn.) In the Expression Suite, you find designer tools that allow you to draw items in a graphics program and export your final graphics in a XAML format. Expression Design was the tool used to create the user controls in this example.

+   4. Add another user control to the project; name it RedX.xaml.

+   5. Replace the XAML in the RedX.xaml file with this XAML:

```
```xml
<UserControl x:Class="BindingSample.RedX"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
    xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
    mc:Ignorable="d"
    d:DesignHeight="50" d:DesignWidth="50">

    <Canvas Width="44.625" Height="45.9394">

        <Path x:Name="Line1Path" Width="44.625" Height="44.375"
              Canvas.Left="0" Canvas.Top="0" Stretch="Fill"
              Fill="#FFD0D09" Data="F1 M 0.3,5L 3.5,0L 44.625,41.42L 42.125,44.375"/>

        <Path x:Name="Line2Path" Width="43.5772" Height="45.3813"
              Canvas.Left="0.20177" Canvas.Top="0.55809"
              Stretch="Fill"
              Fill="#FFD0D09" Data="F1 M 3.7719,45.9394L 0.20177,42.5115L 40.353,0.55809L 43.7784,2.98667"/>

    </Canvas>
</UserControl>
```
```

+   6. Add a new class called BooleanToIconConverter.cs.

+   7. Add the following using statement to your class:

```
```csharp
using System.Windows.Data;
```
```

+   8. Have the BooleanToIconConverter inherit the IValueConverter interface. In the Convert method, if the value passed in is True, have it return a new instance of the GreenCheck user control. If the value passed in is False, have the Convert method return an instance of the RedX user control. Here's the code for the BooleanToIconConverter class:

```
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Windows.Data;

namespace BindingSample
{
    public class BooleanToIconConverter : IValueConverter
    {
        public object Convert(object value, Type targetType,
```
```