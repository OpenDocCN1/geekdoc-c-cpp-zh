```
<UserControl x:Class="BindingSample3.RedX"
xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
mc:Ignorable="d" d:DesignHeight="50" d:DesignWidth="50">

    <Canvas Width="44.625" Height="45.9394">

        <Path x:Name="Line1Path" Width="44.625" Height="44.375" Canvas.Left="0" Canvas.Top="0" Stretch="Fill" Fill="#FFDE0909" Data="F1 M 0,3.5L 3.5,0 44.625,41.125,44.375"/>

        <Path x:Name="Line2Path" Width="43.5772" Height="45.3813" Canvas.Left="0.20177" Canvas.Top="0.55809" Stretch="Fill" Fill="#4FDE0909" Data="F1 M 3.7719,45.93941 0.20177,42.5115L 40.353,0.55809L 43.7784,2.98867"/>

    </Canvas>
</UserControl>
```

+   6. Add a new class called BooleanToIconConverter.cs.
+   7. Add the following using statement to your class:
+       `using System.Windows.Data;`
+   8. Have the BooleanToIconConverter inherit the IValueConverter interface. In the Convert method, if the value passed in is True, have it return a new instance of the GreenCheck user control. If the value passed in is False, have the Convert method return an instance of the RedX user control.

Here’s the code for the BooleanToIconConverter class:

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Windows.Data;

namespace BindingSample3
{
    public class BooleanToIconConverter : IValueConverter
    {
        public object Convert(object value, Type targetType,
            object parameter,
            System.Globalization.CultureInfo culture)
        {
            if (value != null)
            {
                bool boolValue = (bool)value;
                if (boolValue)
                    return new GreenCheck();
                else
```