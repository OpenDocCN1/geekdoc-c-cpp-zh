
The Rectangle example program shown in Figure 8-7 uses the following XAML code to draw two Rectangles:

```
<Rectangle Width="Auto" Height="Auto" Margin="10"
  Stroke="Red" StrokeThickness="10"
  StrokeDashArray="3,3" StrokeCap="Round"/>
```

```
<Rectangle Width="100" Height="50"
  Stroke="Blue" StrokeThickness="5" Fill="Cyan"
  HorizontalAlignment="Center" VerticalAlignment="Center"/>
```

In the first Rectangle, the Width and Height are set to Auto, the control's Margin property determines the control's size and location. Because the Margin is 10 in this example, the Rectangle is positioned so its edges are 10 pixels from the edges of the Grid that contains it.

In the second Rectangle, the Width and Height are explicitly set. Since the control's HorizontalAlignment and VerticalAlignment properties are both set to Center, the control is given its specified size and centered in its container.

![](img/c9b2d394f4fc2f7e276f6a0a6fa92f6_189_0.png)

FIGURE 8-7

# SUMMARY

This chapter describes WPF's 2D drawing controls. These controls let you draw ellipses, lines, rectangles, and other 2D shapes. Although these controls draw very different shapes, they have much in common such as their Stroke and Fill properties.

Most of these controls are relatively simple, although the Path control with its specialized language can be complex. It's so complex, in fact, that you will probably only use it for relatively simple shapes. For complex shapes you want to use program code to generate the Path's drawing commands.

This chapter finishes the description of WPF controls. The controls described in Chapters 5 through 8 should meet most of your everyday programming needs.

The chapters that follow turn away from specific controls and discuss more general issues. Chapter 9, "Properties," explains in general terms how XAML code can set control properties. Since the examples so far in this book have used properties extensively, you probably already know how to set values for simple properties. Chapter 9 provides more background and explains how to set properties that take values that are objects themselves.

# Properties

The preceding chapters in this book include close to 100 examples that demonstrate all sorts of control properties, methods, events, and other features provided by WPF. To keep those examples as simple and self-contained as possible, I sometimes glossed over some techniques used in the code and deferred them to later chapters.

This chapter covers one of these topics: properties are relatively straightforward, and XAML, C#, and Visual Basic can easily work with them.

Others, however, are more confusing. Some properties don't take values that don't have simple data types as Integer or String, and using them can be confusing, particularly in XAML code.

This chapter describes WPF properties. It explains how you can set even complicated property values in XAML, C#, and Visual Basic code.

# PROPERTY BASICS

The idea of a property is fairly simple: a property is a value that belongs to an object and determines its behavior, appearance, or the data that it represents.

For example, if you create a Person class, it probably has properties like FirstName, LastName, and StreetAddress that define the data that a Person represents.

Using this simple property is easy. For example, the following C# code creates a Person object and sets its FirstName and LastName properties:

```csharp
// Create a new Person object.
Person author = new Person();

// Set the Person's name properties.
author.FirstName = "Rod";
author.LastName = "Stephens";
```

# 154 | CHAPTER 9 PROPERTIES

XAML code also handles these kinds of simple-valued properties easily. The following XAML code sets a Label control's Background property to yellow:

```xml
<Label Content="Hello" Background="Yellow"/>
```

Using this kind of simple property is easy in your code, but behind the scenes, WPF is doing a bit more work than you might think. To translate XAML values into something comprehensible behind the scenes, WPF uses type converters.

# TYPE CONVERTERS

While your XAML code simply sets a Label control's Background property to the string "Yellow", the Background property is not a simple string. It is actually an object that is an instance of the System.Windows.Media.Brush class.

The following C# code sets the grdMain control's Background property. Notice that the code doesn't set the property to a string value; instead it uses a static value provided by the Brushes class. The class's Yellow property returns a SolidColorBrush (which is a type of Brush) that has the color yellow.

```csharp
grdMain.Background = Brushes.Yellow;
```

Fortunately, WPF provides a set of type converters that can convert strings like "Yellow" into objects like brushes.

XAML provides type converters for many simple property types such as numbers (Width, Height), points, arrays of points (the Polygon's Points property), numeric arrays (DashArray), strings (the Content property when set to a string), simple colors arrays (Background, Stroke, Fill), Booleans (IsChecked, IsEnabled), simple brushes (the Button.BorderBrush), and many others.

XAML even has a type converter to translate a complex sequence of commands in the Path-language to a series of objects that draw lines, arcs, and curves. For example, the XAML code draws the shape in Figure 9-1. The type converter translates the complex series of arc commands in the Path Data attribute into the curves shown in the figure. (For more information on the Path Data, see "Path Data").

![](img/c9b2d394f4fc2f7e276f6a0a6fa92f6_191_0.png)

FIGURE 9-1

```xml
<Path Fill="HotPink" Stroke="Red" StrokeThickness="3"
      Data="M10,60 A50,50 0 0,1 60,10 A50,50 0 0,1 10,60"/>
```

# PROPERTY ELEMENT SYNTAX

Unfortunately, XAML does not provide type converters for complicated properties. For example, it's easy to describe a single-color Brush with a string such as Yellow, LightGreen, or #FF00CC. But if you want to fill a Grid with the brush shown in Figure 9-2, it would be difficult to represent this complex object as a simple string.

To use complex objects in XAML, you need to build the actual objects instead of describing them in a string. You can do that with property element syntax.

Property element syntax lets XAML code represent a property as a separate element with its own start and end tags inside the object it will use. In example, the Grid that will use the background contains a new element that defines the background.

The property name consists of the control's type (Grid), followed by a dot (.), followed by the property's name (Background); thus, in this case, the element's name is Grid.Background.

Inside this property element, the XAML code defines how the Brush displays the background shown in Figure 9-2:

```xml
<Grid>
  <Grid.Background>
    <GradientBrush>
      <GradientStop Color="#FFFFFF" Offset="0.00"/>
      <GradientStop Color="#FFFF00" Offset="0.25"/>
      <GradientStop Color="#FFFFFF" Offset="0.50"/>
      <GradientStop Color="#FF00FF" Offset="0.75"/>
      <GradientStop Color="#FF000FF" Offset="1.00"/>
    </GradientBrush>
  </Grid.Background>
</Grid>
```

![](img/c9b2d394f4fc2f7e276f6a0a6fa92f6_192_0.png)

FIGURE 9-2

The Grid.Background element is the Grid's background property. It contains a GradientBrush object. That object contains five stops that indicate the colors that the brush should use at various positions. The GradientStop objects' Color and Offset properties are relatively simple values (simple colors) and they are represented as attributes that XAML's type converters can handle.

```csharp
GradientBrush br = new RadialGradientBrush();
br.GradientStops.Add(new GradientStop(Colors.White, 0.00));
br.GradientStops.Add(new GradientStop(Colors.Red, 0.25));
br.GradientStops.Add(new GradientStop(Colors.Yellow, 0.50));
```
