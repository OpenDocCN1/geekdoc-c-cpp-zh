# Listing 9.9: Writing the XAML Code to Add the Buttons in the WPFWindows Application

```
<window x:Class="WPFWindows.MainWindow"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    Title="FirstWindow" Height="300" Width="300">
    <Grid>
        <Button Height="23" Width="100" Name="ChangeLocation" Click="ChangeLocation_Click" VerticalAlignment="Top" HorizontalAlignment="Left" Margin="15,20,0,0">ChangeLocation</Button>
        <Button Height="23" Width="100" Name="AutoFit" Click="AutoFit_Click" VerticalAlignment="Top" Margin="15,60,0,0" HorizontalAlignment="Left">AutoFit</Button>
        <Button Height="23" Width="100" Name="ChangeBorder" Click="ChangeBorder_Click" Margin="15,100,0,0" VerticalAlignment="Top" HorizontalAlignment="Left">ChangeBorder</Button>
        <Button Height="23" Width="100" Name="AnotherWindow" Click="AnotherWindow_Click" Margin="15,140,0,0" VerticalAlignment="Top" HorizontalAlignment="Left">AnotherWindow</Button>
        <Button Height="23" Width="100" Name="Exit" Click="Exit_Click" Margin="15,180,0,0" VerticalAlignment="Top" HorizontalAlignment="Left">Exit</Button>
    </Grid>
</window>
```

In Listing 9.9, the Title property of MainWindow (the default window) is set to FirstWindow and the Height and Width properties are set to 300. The ChangeLocation, AutoFit, ChangeBorder, AnotherWindow, and Exit buttons have the Click property set to the respective handlers for the Click event of the buttons.

Now, let’s set the properties of MainWindow in the Click event handlers of the five buttons.

+   9. Add the code given in Listing 9.10 to write the event handlers of the Click event of the five buttons in the code-behind file (MainWindow.xaml.cs):

# Listing 9.10: Setting the Properties of MainWindow

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

namespace WPFWindows
{
    /// <summary>
    /// Interaction logic for MainWindow.xaml
    /// </summary>
    public partial class MainWindow : Window
    {
        public MainWindow()
        {
            InitializeComponent();
            this.WindowStartupLocation = WindowStartupLocation.CenterScreen;
            this.WindowState = WindowState.Maximized;
        }
        private void ChangeLocation_Click(object sender, RoutedEventArgs e)
        {
            this.WindowState = WindowState.Normal;
            this.Top = 250;
```