The code uses resources to set the window background brush, font, and title. Giving the skins different backgrounds and titles makes it easier to see the skins at a glance.

Next, the code defines a StackPanel containing a series of Buttons. Buttons' Visibility properties are set using resources defined in the skin resource dictionaries. The basic dictionary resBasics.xaml sets Visibility = Collapsed for all of the buttons. The other dictionaries override these settings to display the appropriate buttons. For example, in the Order Entry dictionary, resOrder.xaml, the values CreateOrder and TrackOrder are set to Visible so 'Create Order' and 'Track Order' buttons are shown in the order entry.

The following code shows the resBasics.xaml resource dictionary that defines common values for all of the skins. With the window's font and the character style. It also adds help of

```
<ResourceDictionary
xmlns="http://schemas.microsoft.com/winx/2006/xml/presentation"
xmlns:x="http://schemas.microsoft.com/winx/2006/xml"
xmlns:sys="clr-namespace:System;assembly=mscorlib">

<!-- main window -->
  <FontFamily x:Key="Font">Comic Sans MS</FontFamily>
  <FontWeight x:Key="FontWeight">Bold</FontWeight>
  <sys:Double x:Key="FontSize">18</sys:Double>
  <sys:String x:Key="Title">Ordering</sys:String>

  <!-- Buttons style -->
  <Style TargetType="Button">
    <Setter Property="Width" Value="200"/>
    <Setter Property="Height" Value="50"/>
    <Setter Property="Margin" Value="10"/>
  </Style>

  <!-- Button visibility -->
  <Visibility x:Key="UnshippedOrders">Collapsed</Visibility>
  <Visibility x:Key="CreateOrder">Collapsed</Visibility>
  <Visibility x:Key="FindCustomer">Collapsed</Visibility>
  <Visibility x:Key="TrackOrder">Collapsed</Visibility>
  <Visibility x:Key="SystemMaintenance">Collapsed</Visibility>
</ResourceDictionary>
```

![](bbox=[0.082, 0.345, 0.158, 0.415])

The following code shows the resOrderEntry.xaml skin resource dictionary. It defines the Window's background brush and title, and the Button visibilities for the order entry skin.

```
<ResourceDictionary
xmlns="http://schemas.microsoft.com/winx/2006/xml/presentation"
xmlns:x="http://schemas.microsoft.com/winx/2006/xml"
xmlns:sys="clr-namespace:System;assembly=mscorlib">

  <!-- main window -->
  <LinearGradientBrush x:Key="BrWindow" StartPoint="0,0" EndPoint="0,1">
    <GradientStop Color="LightBlue" Offset="0"/>
    <GradientStop Color="Blue" Offset="1"/>
  </LinearGradientBrush>
```

![](bbox=[0.082, 0.818, 0.158, 0.888])

Ordering