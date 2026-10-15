![](bbox=[0.14, 0.09, 0.58, 0.34])

# FIGURE 19-7

As you can see, there is a lot of power in the Grid control; but it is not just limited to a column and row structure. One thing that the Grid control can offer that none of the other layout controls can offer is anchoring. As you saw in Chapter 15, anchoring is extremely useful for placing controls on user controls that may be resized. For example, if you wanted to place a button in the center of the grid, you would define it like this:

```
<UserControl x:Class="SilverlightApplication1.SilverlightControl1"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
    xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
    mc:Ignorable="d"
    d:DesignHeight="300" d:DesignWidth="400">

    <Grid x:Name="LayoutRoot" Background="White">
        <Button Content="Button" Width="100" Height="30" HorizontalAlignment="Center"
            VerticalAlignment="Center" />
    </Grid>
</UserControl>
```

Code snippet from SilverlightControl1.xaml

Once you have the button centered, you can set the HorizontalAlignment option to Center, Left, Right, or Stretch; and you can set the VerticalAlignment option to Center, Top, Bottom, or Stretch. This will place your button in relation to the Grid control. This is great for placing the control in the bottom-right corner, but sometimes you may not want it directly on the bottom and all the way to the right. This is where margins come into play. For example, if you want to place the button in the bottom-right corner and offset it by 12 pixels from the bottom and the right, you would define it like this:

```
<UserControl x:Class="SilverlightApplication1.SilverlightControl1"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
    xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
    mc:Ignorable="d"
    d:DesignHeight="300" d:DesignWidth="400">

    <Grid x:Name="LayoutRoot" Background="White">
```