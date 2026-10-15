# Listing 9.1 MainPage.xaml—Animated Page Transitions

```
<phone:PhoneApplicationPage
    x:Class="NavigationBars.MainPage"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    xmlns:phone="
        clr-namespace:Microsoft.Phone.Controls;assembly=Microsoft.Phone"
    xmlns:shell=
        "clr-namespace:Microsoft.Phone.Shell;assembly=Microsoft.Phone"
    xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
    xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
    mc:Ignorable="d" d:DesignWidth="480" d:DesignHeight="768"
    FontFamily="{StaticResource PhoneFontFamilyNormal}"
    FontSize="{StaticResource PhoneFontSizeNormal}"
    Foreground="{StaticResource PhoneForegroundBrush}"
    SupportedOrientations="Portrait" Orientation="Portrait"
    shell:SystemTray.IsVisible="True">
    <phone:PhoneApplicationPage.Resources>
        <Storyboard x:Name="openDoorStoryBoard">
            <DoubleAnimation Storyboard.TargetName="gridPlaneProjection"
                             Storyboard.TargetProperty="RotationY"
                             From="0"
                             To="90"
                             Duration="0:0:1"/>
        </Storyboard>
        <Storyboard x:Name="closeDoorStoryBoard">
            <DoubleAnimation Storyboard.TargetName="gridPlaneProjection"
                             Storyboard.TargetProperty="RotationY"
                             From="90"
                             To="0"
                             Duration="0:0:1"/>
        </Storyboard>
    </phone:PhoneApplicationPage.Resources>

    <!--LayoutRoot is the root grid where all page content is placed-->
    <Grid x:Name="LayoutRoot" Background="Transparent">
        <Grid.Projection>
            <PlaneProjection
                x:Name="gridPlaneProjection" CenterOfRotationX="0.0"/>
        </Grid.Projection>
        <Grid.RowDefinitions>
            <RowDefinition Height="Auto"/>
            <RowDefinition Height="*"/>
        </Grid.RowDefinitions>

        <StackPanel x:Name="TitlePanel" Grid.Row="0" Margin="12,17,0,28">
```