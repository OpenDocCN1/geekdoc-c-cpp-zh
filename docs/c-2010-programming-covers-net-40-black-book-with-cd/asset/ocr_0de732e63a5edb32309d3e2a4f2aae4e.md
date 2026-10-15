```
<Line X1="145" X2="145" Y1="145" Y2="166" Stroke="Black" StrokeThickness="5" Height="168" Canvas.Left="-23" Canvas.Top="94" Width="151" />
<Line X1="145" X2="145" Y1="145" Y2="166" Stroke="Black" StrokeThickness="5" Height="168" Canvas.Left="-1" Canvas.Top="94" Width="147" />
<Line X1="11" X2="10" Y1="145" Y2="115" Stroke="Black" StrokeThickness="5" Height="158" Canvas.Left="121" Canvas.Top="-52" Width="42" />
<Polyline Points="10,110 6,10 110,110" Stroke="Black" StrokeThickness="4" Height="52" Canvas.Left="209" Canvas.Top="210" Width="50"/>
<Ellipse Canvas.Left="172" Canvas.Top="118" Height="100" Name="ellipse12" Stroke="Black" Width="87">
<Ellipse.BitmapEffect>
<OuterGlowBitmapEffect GlowColor="DarkViolet" />
</Ellipse.BitmapEffect>
</Ellipse>
<Slider Canvas.Left="22" Canvas.Top="304" Height="21" Name="slider1" Width="339" Value="10" Maximum="100"/>
</Canvas>
</Canvas>
</Window>
```

Now, run the SimpleBindinginWPF application by pressing the F5 key. The output of the SimpleBindinginWPF application is shown in Figure 25.18:

![](bbox=[0.28, 0.38, 0.58, 0.61])

Figure 25.18: Displaying Simple Binding in WPF

In the SimpleBindinginWPF application, the Canvas control is bound to a Slider control. You can move the Canvas control back and forth by moving the Slider control.

# Binding a CLR Object in WPF

To bind a WPF application to a CLR object, you need to define the properties of all the fields used in your application. A CLR object uses the INotifyPropertyChanged interface to implement binding in WPF.

Let’s create a WPF application, named BindingtoCLRObject (also available on the CD) to implement CLR object binding. Perform the following steps to create the BindingtoCLRObject application:

+   1. Create a WPF application, named BindingtoCLRObject.
+   2. Add the code, given in Listing 25.12, to the MainWindow.xaml file:

Listing 25.12: Showing the Code of the MainWindow.xaml file in the BindingtoCLRObject Application

```
<Window x:Class="BindingtoCLRObject.MainWindow"
xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
Title="MainWindow" Height="300" Width="300">
<Grid Name="nameGrid" Margin="5,5,5,5" >
<Grid.ColumnDefinitions>
```