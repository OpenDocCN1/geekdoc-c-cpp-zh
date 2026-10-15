# Using the MediaElement Control

As you know, the MediaElement control allows you to host an audio or video or both in a Silverlight application. Perform the following steps to learn how to use the MediaElement control:

+   1. Create a Silverlight application named MyMediaPlayerAppCS (available on the CD) that is hosted in a single HTML page. Before that, you need to add the media file that you want to play in the current project folder. To do this, you need to use the Add Existing Item dialog box. After adding the media file, select it in Solution Explorer and press the F4 key on the keyboard. The Properties window appears (Figure 17.36).

+   2. Select the Copy to Output Directory property in the Properties window to change the default value of the Copy to Output Directory property from the Do not copy option to the Copy if newer option, as shown in Figure 17.36:

![](bbox=[0.285, 0.26, 0.785, 0.505])

The Copy if newer option copies a media file to the current project folder if the media file is new.

+   3. Now, open the MainPage.xaml file of the application, MyMediaPlayerAppCS, and type the code to use the MediaElement control. Listing 17.9 shows the code for the MainPage.xaml file of the MyMediaPlayerAppCS application:

# Listing 17.9: Showing the Code for the MainPage.xaml File

```
<UserControl x:Class="MyMediaPlayerAppCS.MainPage"
xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
mc:Ignorable="d"
d:DesignHeight="600" d:DesignWidth="600">

<Grid x:Name="LayoutRoot" Background="SteelBlue" DataContext="{Binding}">
<Border BorderBrush="Yellow" BorderThickness="3"/>
<TextBlock Text="My Media Player" HorizontalAlignment="Center" FontSize="24" Margin="0,10,0,0" Foreground="Yellow"/>
<Button x:Name="play" Height="50" Width="50" Content="Play" Margin="0,0,100,425" Background="Yellow" Click="mediaPlay"/>
<Button x:Name="pause" Height="50" Width="50" Content="Pause" Margin="0,0,0,425" Background="Yellow" Click="mediaPause"/>
<Button x:Name="stop" Height="50" Width="50" Content="Stop" Margin="100,0,0,425" Background="Yellow" Click="mediaStop"/>
<Border Height="425" Width="525" BorderBrush="Yellow" BorderThickness="3" Margin="0,100,0,0"/>
<MediaElement x:Name="mediaEle" Height="400" Width="500" Margin="0,100,0,0" Source="wildlife.wmv" Stretch="UniformToFill" Volume="0.75" AutoPlay="False"
```