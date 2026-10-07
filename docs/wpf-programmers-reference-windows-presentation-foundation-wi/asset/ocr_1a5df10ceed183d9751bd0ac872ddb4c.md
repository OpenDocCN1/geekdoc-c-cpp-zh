The PersonSource example program shown in Figure 18-2 uses a binding with its Source property to display information about a Person object.

The PersonSource example program defines a Person class with the properties FirstName, LastName, and NetWork. The program's XAML code includes the namespace definition so you can use the following:

```
xmlns:local=clr-namespace:PersonSource
```

The following code shows how the program's XAML code defines a static resource named a_person as a Person object:

```
<Window.Resources>
  <local:Person xKey="a_person" FirstName="Bill"
    LastName="Gates" NetWork="4000000000"/>
</Window.Resources>
```

![](bbox=[0.64, 0.101, 0.871, 0.253])

The following code shows how the program uses bindings to display the Person object's FirstName, LastName, and NetWork values. Each binding Source property identifies the Person object provides:

```
<Label Grid.Row="1" Grid.Column="0" Content="First Name"/>
<Label Grid.Row="1" Grid.Column="1"
  Content={Binding Source=StaticResource a_person, Path=FirstName}/>
<Label Grid.Row="2" Grid.Column="0" Content="Last Name"/>
<Label Grid.Row="2" Grid.Column="1"
  Content={Binding Source=StaticResource a_person, Path=LastName}/>
<Label Grid.Row="3" Grid.Column="0" Content="NetWork"/>
<Label Grid.Row="3" Grid.Column="1"
  Content={Binding Source=StaticResource a_person, Path=NetWork}/>
```

![](bbox=[0.64, 0.506, 0.871, 0.683])

# RelativeSource

The binding's RelativeSource property lets you specify a source object by its relationship to the target control. One situation in which this is useful is you want to bind two properties on the same control.

The TypeColor example program shown in Figure 18-3 shows the TextBox's Background property to its Text property, so when you type the name of a color, the control colors as its background.

![](bbox=[0.64, 0.809, 0.871, 0.936])