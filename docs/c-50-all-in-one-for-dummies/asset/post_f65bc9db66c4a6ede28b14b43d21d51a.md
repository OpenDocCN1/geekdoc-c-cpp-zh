
# Investigating the Binding Object 603

the source property value will not update the target property. However, updates to the target property value will automatically update the source property value.

- **The TwoWay binding mode merges the functionality of the OneWay and OneWayToSource binding modes. In this binding mode, the source property value initializes the target property value. Subsequent changes to the source property value update the target property value. Similarly, updates to the target property value will update the source property value.**

# Investigating the Binding Object

Bindings can be defined using code or XAML. Here you begin with the XAML version. In order to see how to bind to a UI element, you first define a test set to work with.

![](img/6df7bb88e9302e98442acc219cfbd7fc_628_0.png)

The complete solution is available at www.csharpfordummies.net in the chapter downloads under BindingSample1.

# Defining a binding with XAML

Just follow these steps to create a binding with XAML:

- **1. Create a new WPF Application project and name it BindingSample1.**
- **2. Define a named Car class by adding a new Class to your solution named Car.cs and code it as follows:**

```c
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

namespace BindingSample1
{
    public class Car
    {
        private string _make;
        public string Make
        {
            get { return _make; }
            set { _make = value; }
        }
        private string _model;
        public string Model
        {
            get { return _model; }
            set { _model = value; }
        }
        public Car() { }
    }
}
```

# 604 Investigating the Binding Object

- 3. In MainWindow.xaml, replace the grid with one that defines a double column and single row grid; then add a label in each grid cell, like this:

```xml
<Grid>
  <ColumnDefinitions>
    <ColumnDefinition></ColumnDefinition>
    <ColumnDefinition></ColumnDefinition>
  </ColumnDefinitions>
  <RowDefinitions>
    <RowDefinition />
  </RowDefinitions>
  <Label Name="lblCarMake" Grid.Row="0" Grid.Column="0" Content="{Binding Path=Make, Mode=OneWay}" />
  <Label Name="lblCarModel" Grid.Row="0" Grid.Column="1" Content="{Binding Path=Model, Mode=OneWay}" />
</Grid>
```

Take a look at the Content property value. The information contained within the query braces the binding to be displayed in the labels. I describe what this Binding expression means in the next section, but first you need some data to bind to.

- 4. Open the MainWindow.xaml.cs code-based file and create a method called GenerateData that instantiates a Car object and assigns it to the DataContext of the value, like this:

```csharp
private void GenerateData() {
  Car car = new Car( Make = "Alon", Model = "XYZ" );
  this.DataContext = car;
}
```

![](img/6df7bb88e9302e98442acc219cfbd7fc_629_0.png)

DataContext defines the root object relative to all child elements obtain their values (as long as the DataContext value on the child elements is not directly set via XAML or property — this is an example of property inheritance; its value is obtained from its parent element unless otherwise specified).

- 5. Call the GenerateData() method in the MainWindow constructor (public MainWindow()), immediately following InitializeComponents().

Now, looking back to the XAML file (MainWindow.xaml), the first lblCarMake will bind to the DataContext's Make property. The value is retrieved from the property specified in the binding's Path component; the second label lblCarModel will bind to the DataContext's Model property as specified in the binding expression's Path property using a OneWay mode, which means the label content will be bound only once, regardless of the underlying object being bound to changes.

![](img/6df7bb88e9302e98442acc219cfbd7fc_629_1.png)

The Path component of the XAML Binding simply tells the XAML processor to extract its value from a specific property of its DataContext. The Path value can also express properties that are nested, as in the case of nested complex objects. In these cases,

# Investigating the Binding Object 605

you use dot notation to reach the desired property, such as Property.SomeObject.SomeOtherProperty.

- 6. Run the application.

You can see that the labels now display the Make and Model of the Car object that was assigned to the DataContext of the window. (See Figure 3-1.)

![](img/6df7bb88e9302e98442acc219cfbd7fc_630_0.png)

Figure 3-1: Data binding to a Data-Context.

# Defining a binding with C#

You can also use C# to define bindings. To demonstrate this, remove the Content entirely from both labels in the XAML file. The label markup should now resemble the following:

```xml
<Label Name="lbiCarMake" Grid.Row="0" Grid.Column="0" />
<Label Name="lbiCarModel" Grid.Row="0" Grid.Column="1" />
```

Modify the GenerateData() method in MainWindow.xaml to implement the Binding definitions code. To do this, you must instantiate Binding objects directly. The constructor of the Binding object takes the string Path value. Use the BindingOperations class to apply the Binding to the Content dependency property of your labels.

BindingOperations is a helper class provided to you by WPF. It has static methods that give you the power to add and clear data binding definitions on application elements.

The following code shows how to define the Binding objects, and assign the binding to the Content of the labels:

```csharp
private void GenerateData()
{
    Car car1 = new Car() { Make = "Athlon", Model = "XYZ" };

    Binding bindingBinding = new Binding("Make");
```

# 606 Editing, Validating, Converting, and Visualizing Your Data

```csharp
makeBinding.Mode = BindingMode.OneTime;
BindingOperations.SetBinding(lblCarMake,
Label.ContentProperty, makeBinding);
```

```csharp
Binding modelBinding = new Binding("Model");
modelBinding.Mode = BindingMode.OneTime;
BindingOperations.SetBinding(lblCarModel,
Label.ContentProperty, modelBinding);
```

```csharp
this.DataContext = car;
```

![](img/6df7bb88e9302e98442acc219cfbd7fc_631_0.png)

Dependency properties are typically defined with the "Property" suffix, but you only see them when navigating through code. This section builds on this by using TwoWay mode so that changes made to the Car object will be reflected in the user interface. The complete solution is available at www.csharpfordummies.net in the chapter downloads under BindingSample1.
