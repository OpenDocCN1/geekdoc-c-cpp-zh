down to the child element that originally raises the event, that is, from outer element to inner element. Tunneling events are also known as preview events as the names of the events are prefixed with Preview, as shown in Listing 9.6:

# Listing 9.6: Demonstrating the Traversal of a Tunneling Event

```
<Window x:Class="MyWpfApplication.MainWindow"
xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
Title="MainWindow" Height="350" Width="525"
PreviewMouseRightButtonUp="MouseRightHandler">
<Grid Name="grid1" PreviewMouseRightButtonUp="MouseRightHandler">
<Button Name="button1" Height="25" Width="75" Content="button1" Margin="100,10,100,220" PreviewMouseRightButtonUp="MouseRightHandler"/>
<Button Name="button2" Height="150" Width="150" Margin="0" PreviewMouseRightButtonUp="MouseRightHandler">
<Grid Name="grid2" Height="100" Width="100" PreviewMouseRightButtonUp="MouseRightHandler">
<TextBox Name="textBox1" Text="textBox1" Height="25" Margin="0,0,45,60" PreviewMouseRightButtonUp="MouseRightHandler"/>
<TextBox Name="textBox2" Text="textBox2" Height="25" Margin="45,60,0,0" PreviewMouseRightButtonUp="MouseRightHandler"/>
</Grid>
</Button>
<Button Name="button3" Height="25" Content="button3" Margin="100,220,100,10" PreviewMouseRightButtonUp="MouseRightHandler"/>
</Grid>
</Window>
```

In Listing 9.6, you can see that the PreviewMouseRightButtonUp event is associated with its handler, MouseRightHandler, in all the elements. The PreviewMouseRightButtonUp event is a tunneling routed event that is available to all the elements derived from the UIElement class. Whenever you right click any element, the PreviewMouseRightButtonUp event occurs on the root element and tunnels down to the source element. Figure 9.33 provides a visual representation of the traversal of the PreviewMouseRightButtonUp event:

![](bbox=[0.22, 0.56, 0.92, 0.88])

# Figure 9.33: Traversal of PreviewMouseRightButtonUp Routed Event