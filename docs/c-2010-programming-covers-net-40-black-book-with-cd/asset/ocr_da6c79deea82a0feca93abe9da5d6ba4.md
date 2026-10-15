Storyboard timeline from the point it had been paused. The Seek button starts increasing the width of the ellipse from the point specified in the Origin property. The SkipToFill button fills the area of the Storyboard timeline by jumping to the last point. You can see the output in Figure 12.33:

![](bbox=[0.29, 0.13, 0.73, 0.32])

Figure 12.33: Controlling Storyboard in XAML

# Controlling Storyboard Using Code-Behind Code

When you are controlling the Storyboard timeline through code, you must create a NameScope class for a FrameworkElement class to register the names of the objects to animate with the FrameworkElement class. To start an animation in code, you should use the BeginStoryboard property with an EventTrigger object. You can also use an event handler and the Begin() method of the Storyboard class. You can create the same effect as XAML through the code-behind code as well. Let’s create an animation in which you can control the Storyboard timeline through code. To do this, create a WPF application named Storyboard_Code (also available in CD) and add the code, given in Listing 12.30, to the MainWindow.xaml file:

# Listing 12.30: Adding a Button Using the XAML Code

```
<window x:class="Storyboard_Code.MainWindow"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    Title="MainWindow" Height="300" Width="300">
    <Grid>
        <Button Width="100" Name="button1" Click="button1_Click"
            HorizontalAlignment="Left" Margin="0,27,0,0" Height="29"
            VerticalAlignment="Top">Click to grow</Button>
    </Grid>
</Window>
```

The code in Listing 12.30 is the XAML code, which is used to add a Button named button1 to the application. The button1 control is animated in the code-behind file. Add the code, given in Listing 12.31, to the MainWindow.xaml.cs file:

# Listing 12.31: Animating a Button Control

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Windows;
using System.Windows.Controls;
using System.Windows.Data;
using System.Windows.Documents;
using System.Windows.Input;
using System.Windows.Media;
using System.Windows.Media.Imaging;
using System.Windows.Navigation;
using System.Windows.Shapes;
using System.Windows.Media.Animation;
```