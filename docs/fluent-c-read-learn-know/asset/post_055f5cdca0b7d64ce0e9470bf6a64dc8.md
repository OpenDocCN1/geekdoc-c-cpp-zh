
![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_515_0.png)

## XAML FUNDAMENTALS

Let's start our examination of XAML with a comparison of XAML markup with something you're already familiar with, C#. The following code snippets produce the same window:

```xml
<Window x:Class="MainWindow" Title="My Window" Name="MyWindow">
  <Grid Name="LayoutRoot">
    <!-- The button is inside the grid -->
    <Button Name="FirstButton" Height="74" Width="229">
      Click Me, Please
    </Button>
  </Grid>
</Window>
```

```csharp
Window MyWindow = new MainWindow();
MyWindow.Title = "My Window";
Grid LayoutRoot = new Grid();
MyWindow.Content = LayoutRoot;
// The button is inside the grid
Button FirstButton = new Button();
FirstButton.Height = 74;
FirstButton.Width = 229;
FirstButton.Content = "Click Me, Please";
LayoutRoot.Children.Add(FirstButton);
```

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_515_1.png)

### PUT ON YOUR THINKING HAT

If C# can do everything XAML can do, and a lot more besides, can you think of some reasons why using both languages in the application development process is a good idea?

### HOW'D YOU DO?

Did you think of some reasons? Were you convinced by them? Here's a list of a few you might not have thought of:

### XAML IS OFTEN MORE CONCISE

If you compare the snippets on the previous page, you'll see that the XAML version of the window is much less verbose. (But that's not always true.)

### XAML IS DECLARATIVE

"Declarative" doesn't necessarily mean better, but it's often easier to understand (and write). Imagine the difference between saying "I want an electrical outlet on that wall" and actually wiring it.

### XAML CLEARLY EXPRESSES THE WPF COMPOSITION MODEL

As we'll see when we explore logical and visual trees, WPF interfaces are composed. Things don't just float around on their own: a String is contained in a Button that's contained in a Grid that's contained in a Window. The hierarchical structure of XAML makes that much, much clearer than procedural code.

### XAML IS TOOLABLE

The folks at Microsoft talk about XAML being "toolable". What they mean is that because XAML is plain old XML it can be easily parsed and manipulated by any application. A great example of that is Microsoft's Expression Blend, a designing and prototyping tool aimed at designers rather than developers (for which read, "it will feel familiar to people used to working in Adobe Photoshop").

### XAML SUPPORTS SEPARATE WORKFLOWS

Programmers, as a class of people, aren't known for their graphic design skills; it's a different profession. But once you have separate tools for designing the graphics and implementing the behavior, it becomes trivially simple to let different people perform the tasks they're trained to do. Doesn't it make sense to let the graphic designers design, and the programmers program? XAML makes that easy. And because many graphic designers are familiar with another XML-based language, HTML, many of them find working directly in XAML quite comfortable.

### SYNTAX BASICS

If you're familiar with XML or HTML the syntax of XAML will already be familiar, but it adds some extensions to basic XML and uses some special vocabulary. If you're not familiar with XML don't worry. It's really, really easy.

### OBJECT ELEMENTS

The basic unit of C# is a statement. The basic unit of XAML is an object element. Just as in C# you can write single- or multi-line statements, you can write single- and multi-line object element declarations:

This syntax is used for elements that don't contain any other elements. It's roughly equivalent to a single-line C# statement.

```xml
<Button />
```

This syntax is used when other elements are nested inside the object. It's roughly equivalent to a C# statement block surrounded by braces.

```xml
<Button>
  <Element />...
</Button>
```

### ATTRIBUTES AND PROPERTIES

In C#, you assign a value to the property of an object using syntax like Object.Property = value. In XAML, you have two options. You can either set the property as an attribute that's declared in the opening tag, or you can define the property as a separate nested element:

This is ATTRIBUTE SYNTAX Attributes are contained in quotation marks, and multiple attributes are separated by white space.

```xml
<Button Height="74" Width="229" />
```

This is called PROPERTY ELEMENT SYNTAX. For some complex attributes, it's a lot easier to write and understand than attribute syntax.

```xml
<Button Width="229">
  <Button.Height>74</Button.Height>
</Button>
```

Notice that you can combine property element and attribute syntax.

### CONTENT PROPERTIES

Did you notice that in the Button property element example, we had to specify the Height property as Button.Height?

When we used attribute syntax, we only had to specify the property name.

```xml
<Button Width="229">
  <Button.Height>74</Button.Height>
</Button>
```

Property element syntax required the object name and the property name.

Repeating the object name like that makes it clear that you're referring to a property, not some other element named “Height”. But every WPF element can define a single property, called the content property, that can simply be placed between the opening and closing tags of the object. For the Button, the content property is whatever’s displayed inside the Button, usually a string:

```xml
<Button>
  Click Me, Please
</Button>
```

The content property doesn’t need to be enclosed in tags (although you can), and some elements, like the WPF Button, can even interpret string directly without enclosing them in quotes.

The tricky bit about using the content property is knowing what it means. Technically, the content property is any object that will be displayed by the ContentPresenter of the control’s template. (We’ll examine control templates in Chapter 21.) It’s usually intuitive, though, like the Button. I mean, what else would you expect the control to do with “Click Me, Please” but display it?

### PUT ON YOUR THINKING HAT

Time to get your feet wet. Can you translate the C# snippet below into XAML, and the XAML code into C#? [Don't worry about what all the elements are. We'll be examining them in later chapters.]

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_519_0.png)

```csharp
Window MainWindow = new MainWindow();
MainWindow.Title = "Sample";
MainWindow.Height = 300;
MainWindow.Width = 500;

DockPanel LayoutRoot = new DockPanel();

Menu MainMenu = new Menu();
MenuItem FileMenu = new MenuItem();
FileMenu.Header = "File";

MainMenu.AddChild(FileMenu);
LayoutRoot.Children.Add(MainMenu);
MainWindow.Content = LayoutRoot;
```

> Notice that you call AddChild() on the Menu, but Add() on the LayoutRoot. You'll find out why when we examine WPF controls in the next chapter.

```xml
<Window x:Class="MainWindow" Height="Auto" Width="Auto">
  <Grid Name="LayoutRoot">
    <Button Height="50" Width="75">
      Cancel
    </Button>
  </Grid>
</Window>
```

### HOW'D YOU DO?

Remember, there are different ways to express the same thing in both C# and XAML, so don't worry if your code is a little different than mine, so long as the syntax is correct.

```csharp
Window MainWindow = new MainWindow();
MainWindow.Title = "Sample";
MainWindow.Height = 300;
MainWindow.Width = 500;
DockPanel LayoutRoot = new DockPanel();
Menu MainMenu = new Menu();
MenuItem FileMenu = new MenuItem();
FileMenu.Header = "File";
MainMenu.AddChild(FileMenu);
LayoutRoot.Children.Add(MainMenu);
MainWindow.Content = LayoutRoot;
```

```xml
<Window x:Class="MainWindow" Title="Sample" Height="300" Width="500">
  <DockPanel Name="LayoutRoot">
    <Menu Name="MainMenu">
      <MenuItem Name="FileMenu" Header="File" />
    </Menu>
  </DockPanel>
</Window>
```

This one was a little tricky. Did you get it right? You don't need to explicitly add the MenuItem to the Menu because that's implicit in the structure of the XAML.

Did you have a problem figuring out what to call the variables here? Unlike C# variables, XAML elements don't have to have names unless you're going to reference them in code, but it's a good idea to give them one using the name attribute.

```csharp
MainWindow myWindow = new MainWindow();
Grid LayoutRoot = new Grid();
Button myButton = new Button();
myButton.Height = 50;
myButton.Width = 75;
LayoutRoot.Children.Add(myButton);
myWindow.Content = LayoutRoot;
```

```xml
<Window x:Class="MainWindow" Height="Auto" Width="Auto">
  <Grid Name="LayoutRoot">
    <Button Height="50" Width="75">
      Cancel
    </Button>
  </Grid>
</Window>
```
