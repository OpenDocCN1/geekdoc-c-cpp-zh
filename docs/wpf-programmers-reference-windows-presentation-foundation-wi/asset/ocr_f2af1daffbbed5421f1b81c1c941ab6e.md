For example, the PersonSource example program described earlier in this chapter and shown in Figure 18-2 uses several Label controls to display a Person object's property values. The following code shows how one of the Labels is defined:

```
<Label Grid.Row="1" Grid.Column="1"
Content="Binding Source=(StaticResource a_person), Path=FirstName)"/>
```

Each of the Labels uses a similar binding that includes its source.
The PersonSource2 example program is similar it uses DataContext properties to simplify the Labels' bindings. The following code shows how the DataContext property for the Grid that contains the Labels. The code binds the Grid's DataContent property to the a_person object.

```
<Grid Margin="10" DataContext="Binding Source=(StaticResource a_person)"/>
```

The following code shows the new Label definition with its simplified binding:

```
<Label Grid.Row="1" Grid.Column="1" Content="(Binding Path=FirstName)"/>
```

Because the Label uses the Grid's DataContext, it already has a binding source. The new code only needs to specify the binding's path.
Using DataContext properties in this can simplify the code. It also makes the data source centralized so it's easier to change if you need a different data source.

# Binding Path

Usually a binding path is easy to understand. In many cases, you can set it by setting the Path attribute to the name of the source property that you want to use. For example, the following code sets the binding's path to the txtTypeText TextBox property:

```
<Label Margin="5" BorderRadius="Yellow" BorderThickness="1"
Content="Binding ElementName=txtTypeText, Path=Text"/>
```

The following list summarizes the rules for specifying a binding path:

+   - To use a property of the binding source, set the path equal to the property's name, as in Path = Property.
- If a property is an object, you can use the object's properties, as Path = Object.Property.
- If the path includes an attached property, enclose the property in parentheses. For example, the GridColumns program uses the following code to make a Label display its Grid.Column value:

```
<Label Grid.Column="0" RelativeSource=(RelativeSource Self), Path=(Grid.Column)"/>
```