
## Chapter 3: Data Binding in WPF

### In This Chapter

- Understanding dependency properties
- Working with binding modes
- Defining an example binding object
- Making sense out of data

Data binding allows data from your application objects (the binding source) to be displayed in your user interface elements (the binding target). What this means is that you can bind a Textbox's `Text` property (for example) to the `Name` property of an instance of your `Car` class. Depending on the binding mode used when setting up the relationship, changes in the `Text` property value of the `Textbox` can automatically update the underlying `Name` property of your `Car` object (and vice versa) without requiring any additional code.

It's no mystery these days that most applications deal with data. As a WPF developer, you have full creative reign on how data is presented and how information entered by your user can be validated and used to update your underlying objects. One of WPF's strengths is its rich data binding support. This chapter walks you through the details.

### Getting to Know Dependency Properties

Data binding happens when you set up a relationship between a binding source property and binding target property. The binding target object must be a `DependencyObject`, and the target property must be a `DependencyProperty`.

Understanding dependency properties is crucial to obtaining a firm grasp on WPF technology. Dependency properties are found in objects that inherit from `DependencyObject`. At its root, a dependency property extends the functionality of a regular property that already exists on a CLR object by adding a set of services that is also known as the WPF Property System. (Together, `DependencyObject` and `DependencyProperty` make up this property system.) Dependency properties can have their values determined by multiple input sources, meaning that their values can be obtained through a Style or a data binding expression. Dependency properties act like regular properties, but they allow you to set values based on the following:

- **A default value:** These are predefined on the property.
- **A calculated expression (similar to CSS expressions in the web world):** This can be a data binding expression or a reference to resources defined in the application.
- **Data binding:** This actually is built upon the preceding bullet using binding expressions on the binding source object.
- **Property value inheritance:** Not to be confused with object inheritance, property value inheritance allows values set on parent properties to be propagated down to its children. For instance, if you set FontSize values on the Window element (the root element), child elements such as TextBlock and Label automatically inherit those font property values. You can see another example of this by reviewing the concept of Attached Properties introduced in Chapter 1 of this minibook.
- **Styling:** Each style typically contains setters to set one or more property values.

The WPF property system also provides built-in property value change notification and property value validation functionality, which I review in the section "Editing, Evaluating, Converting, and Visualizing Your Data," later in this chapter.

At the end of the day, dependency properties give the developer the capability to set property values directly in XAML as well as in code. The advantage to this is that you can keep your code clean and leave initializing object property values to XAML.

### Exploring the Binding Modes

You have full control over how the binding relationship you create behaves. Multiple types of binding modes are available to you in WPF. These include the following:

- **The OneTime binding mode** is used when you want the source property to only initially set the target property value. Subsequent changes to the source property are not reflected in the target property. Similarly, changes to the target property are not reflected in the source property.
- **The OneWay binding mode** is typically used for read-only behaving properties. In this binding mode, data from the source property sets the initial value of the target property. Subsequent changes to the source property will automatically update the binding target property value. Conversely, any subsequent changes made to the target property value are not reflected in the source property.
- **The OneWayToSource binding mode** is essentially the opposite of the OneWay binding mode. In this binding mode, data from the source property initializes the target property value. Subsequent changes to the source property value will not update the target property. However, updates to the target property value will automatically update the source property value.
- The TwoWay binding mode merges the functionality of the OneWay and OneWayToSource binding modes. In this binding mode, the source property value initializes the target property value. Subsequent changes to the source property value update the target property value. Similarly, updates to the target property value will update the source property value.

### Investigating the Binding Object

Bindings can be defined using code or XAML. Here you begin with the XAML version. In order to see how to bind data to your UI elements, you first define a test set of data to work with.

![](img/80ff26f06fc9ab951e1cd4257b867366_628_0.png)

The complete solution is available at www.csharpfordummies.net in the chapter downloads under BindingSample1.

### Defining a binding with XAML

Just follow these steps to create a binding with XAML:

- 1. Create a new WPF Application project and name it BindingSample1.
- 2. Define a simple Car class by adding a new Class to your solution named Car.cs and code it as follows:

```csharp
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

- 3. In MainWindow.xaml, replace the grid with one that defines a double column and single row grid; then add a label in each grid cell, like this:

```xml
<Grid>
    <Grid.ColumnDefinitions>
        <ColumnDefinition/><ColumnDefinition/>
    </Grid.ColumnDefinitions>
    <Grid.RowDefinitions>
        <RowDefinition/>
    </Grid.RowDefinitions>
    <Label x:Name="lblCarMake" Grid.Row="0" Grid.Column="0"
        Content="{Binding Path=Make, Mode=OneTime}" />
    <Label x:Name="lblCarModel" Grid.Row="0" Grid.Column="1"
        Content="{Binding Path=Model, Mode=OneTime}" />
</Grid>
```

Take a look at the Content dependency property value. The information contained within the curly braces defines the binding for the content to be displayed in the labels. They describe what this Binding expression means in the next section, but first need some data to bind to.

- 4. Open the MainWindow.xaml.cs code-behind file and create a method called GenerateData that instantiates a Car object and assigns it to the DataContext of the window, like this:

```csharp
private void GenerateData()
{
    Car car1 = new Car() { Make = "Athlon", Model = "XYZ" };
    this.DataContext = car1;
}
```

DataContext defines the root object relative to which all child elements obtain their values (as long as the DataContext value on the child elements isn't directly set via XAML or code — this property is an example of property value inheritance; its value is obtained from its parent element unless otherwise specified).

![](img/80ff26f06fc9ab951e1cd4257b867366_629_0.png)

- 5. Call the GenerateData() method in the MainWindow constructor (public MainWindow()), immediately following InitializeComponent() call.

Now, looking back to the XAML file (MainWindow.xaml), the first label lblCarMake will bind to the DataContext's Make property. The value is retrieved from the property specified in the binding's Path component. Similarly, the second label lblCarModel will bind to the DataContext's Model property as specified in the binding expression's Path property. Each of these bindings is using a OneTime mode, which means the label content will be bound only once, regardless if the underlying object property being bound to changes.

![](img/80ff26f06fc9ab951e1cd4257b867366_629_1.png)
