After defining two grid columns, the code creates a ListBox. Its ItemsSource property is set to the unusual value {Binding} to indicate that this property should be set to the control's inherited DataContext value.

The Label's Content and Background properties are both set to {Binding Path/}; so their binding source is the control's inherited DataContext, and their binding path is the array's selected value.

# BINDING COLLECTIONS

Some controls, as Button, TextBox, and Label, are considered content controls. They are intended to display piece of data as some text or a grid containing other controls.

Other controls, as ListBox, ComboBox, TreeView, are considered item controls. These display a repeating sequence of values stored in collections, arrays, trees, or other repetitive structures. The values can be simple things as numbers or strings, or can be more complex objects as instances of the Order or Employee classes.

Binding controls are relatively straightforward. Set the binding, target property, source, and path; and you're done.

On the surface, binding item controls is just as easy. Just set the control's ItemsSource property to some sort of collection that holds repeating values. If the values are simple numbers or strings, this

The NumberList example program shown in Figure 18-8 works this way.

The NumberList example program defines an array of integers. To define the numbers using the Int32 data type, the program includes the following namespace declaration:

```
xmlns:sys="clr-namespace:System;assembly=mscorlib
```

The program defines its array in its Windows.Resources section:

```
<Window.Resources>
  <x:Array Key="numbers" Type="sys:Int32">
    <sys:Int32>100</sys:Int32>
    <sys:Int32>200</sys:Int32>
    <sys:Int32>50</sys:Int32>
    <sys:Int32>800</sys:Int32>
    <sys:Int32>175</sys:Int32>
  </x:Array>
</Window.Resources>
```

![](bbox=[0.75, 0.465, 0.93, 0.575])

FIGURE 18-8

Finally, we use the following code to bind the array to a ListBox:

```
<ListBox ItemsSource={StaticResource numbers} Background="Transparent">
```

As you can see in Figure 18-8, the ListBox automatically displays the values in the array.