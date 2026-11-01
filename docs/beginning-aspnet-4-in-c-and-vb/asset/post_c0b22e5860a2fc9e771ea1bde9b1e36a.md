
```
CREATE XML INDEX idx_examNumbers on [Exams] ([Info])
    USING XML INDEX idx_exams FOR PATH
```

The PROPERTY index is used if properties are fetched from elements with the value() function. The FOR PROPERTY statement with the index creation defines a PROPERTY index:

```
CREATE XML INDEX idx_examNumbers on [Exams] ([Info])
    USING XML INDEX idx_exams FOR PROPERTY
```

If elements are searched through the tree with an XPath descendant-or-self axis expression, the best performance might be achieved with a VALUE index. The XPath expression //Certification searches all Certification elements with the descendant-or-self axis. The expression [@Name="MCTS ASP.NET Applications"] returns only the elements where the attribute Name has the value MCTS Web Applications:

```
SELECT [Info].query('//Exam/Title/text()') FROM [Exams]
WHERE [Info].exist('//Certification[@Name="MCTS ASP.NET Applications"]') = 1
```

The result returned lists the titles of the exams that contain the requested certification:

```
TS: Microsoft .NET Framework 3.5, ASP.NET Application Development
```

The VALUE index is created with the FOR VALUE statement:

```
CREATE XML INDEX idx_examNumbers on [Exams] ([Info])
    USING XML INDEX idx_exams FOR VALUE
```

## Strongly Typed XML

The XML data type in SQL Server can also be strongly typed with XML schemas. With a strongly typed XML column, it is verified if the data conforms to the schema when XML data is inserted.

A XML schema can be created with the CREATE XML SCHEMA COLLECTION statement. The statement shown here creates a simple XML schema, CourseSchema. The schema defines the type CourseElt that contains a sequence of Number and Title, which are both of type string, and an element Any, which can be any type. Number and Title may occur only once. Because Any has the minOccurs attribute set to 0, and the maxOccurs attribute set to unbounded, this element is optional. This allows you to add any additional information to the CourseElt type in future versions, while the schema still remains valid. Finally, the element name Course is of type CourseElt:

```
CREATE XML SCHEMA COLLECTION CourseSchema AS
'<?xml version="1.0" encoding="UTF-8"?>
<xs:schema id="Courses" targetNamespace="http://thinktecture.com/Courses.xsd"
elementFormDefault="qualified" xmlns="http://thinktecture.com/Courses.xsd"
xmlns:xs="http://www.w3.org/2001/XMLSchema">
<xs:complexType name="CourseElt">
<xs:sequence>
<xs:element name="Number" type="xs:string" maxOccurs="1"
minOccurs="1" />
<xs:element name="Title" type="xs:string" maxOccurs="1"
minOccurs="1" />
<xs:element name="Any" type="xs:anyType"
maxOccurs="unbounded" minOccurs="0" />
</xs:sequence>
</xs:complexType>
<xs:element name="Course" type="CourseElt">
</xs:element>
</xs:schema>
```

With this schema, a valid XML looks like this:

```
<Course xmlns="http://thinktecture.com/Courses.xsd">
  <Number>2549</Number>
  <Title>Advanced Distributed Application Development with Visual Studio 2008
</Title>
</Course>
```

## 35
## Core WPF
### WHAT'S IN THIS CHAPTER?
- Shapes and geometry as the base drawing elements
- Scaling, rotating, and skewing with transformations
- Brushes to fill backgrounds
- WPF controls and their features
- Defining a layout with WPF panels
- Styles, templates, and resources
- Triggers and the Visual State Manager
- Animations
- 3-D

Windows Presentation Foundation (WPF) is a library to create the UI for smart client applications. This chapter gives you broad information on the important concepts of WPF. You can read about a large number of different controls and their categories, how to arrange the controls with panels, customize the appearance using styles, resources, and templates, add some dynamic behavior with triggers and animations, and get an introduction to 3-D with WPF.

### OVERVIEW

One of the big features of WPF is that work can be easily separated between designers and developers. The outcome from the designer’s work can directly be used by the developer. To make this possible, you need to understand eXtensible Application Markup Language, or XAML. You should read Chapter 27, “Core XAML” to get information on this XAML syntax.

The first topic of this chapter gives you an overview of the class hierarchy and categories of classes that are used with WPF, including additional information to understand the principles of XAML. WPF consists of several assemblies containing thousands of classes. So that you can navigate within this vast number of classes and find what you need, the overview explains the class hierarchy and namespaces in WPF.

| NAMESPACE | DESCRIPTION |
|---|---|
| System.Windows.Markup | Helper classes for XAML markup code are located in this namespace. |
| System.Windows.Media | To work with images, audio, and video content, you can use classes in this namespace. |
| System.Windows.Navigation | This namespace contains classes for navigation between windows. |
| System.Windows.Resources | This namespace contains supporting classes for resources. |
| System.Windows.Shapes | The core classes for the UI are located in the System.Windows.Shapes namespace: Line, Ellipse, Rectangle, and the like. |
| System.Windows.Threading | WPF elements are bound to a single thread. In the namespace System.Windows.Threading, you can find classes to deal with multiple threads — for example, the Dispatcher class belongs to this namespace. |
| System.Windows.Xps | XML Paper Specification (XPS) is a new document specification that is also supported by Microsoft Word. In the namespaces System.Windows.Xps, System.Windows.Xps.Packaging and System.Windows.Xps.Serialization, you can find classes to create and stream XPS documents. |

### Class Hierarchy

WPF consists of thousands of classes with a deep hierarchy. For help in understanding the relationship between the classes, see Figure 35-1. Some classes and their functionalities are described in the following table.

![](img/d7d2ffa0a76feaab821930e95daace93_1046_0.png)

FIGURE 35-1

| CLASS | DESCRIPTION |
|---|---|
| DispatcherObject | DispatcherObject is an abstract base class for classes that are bound to one thread. WPF controls require that methods and properties be invoked only from the creator thread. Classes that are derived from DispatcherObject have an associated Dispatcher object that can be used to switch the thread. |
| Application | In a WPF application, one instance of the Application class is created. This class implements a Singleton pattern for access to the application windows, resources, and properties. |
| DependencyObject | DependencyObject is the base class for all classes that support dependency properties. Dependency properties are discussed in Chapter 27, "Core XAML". |
| Visual | The base class for all visual elements is Visual. This class includes features for hit testing and transformation. |
| UIElement | The abstract base class for all WPF elements needing basic presentation features is UIElement. This class provides tunneling and bubbling events for mouse moves, drag and drop, and key clicks. It exposes virtual methods for rendering that can be overridden by derived classes, and it provides methods for layout. WPF does not use Window handles. You can consider this class equivalent to Window handles. |
| FrameworkElement | FrameworkElement is derived from the base class UIElement and implements the default behavior of the methods defined by the base class. |
| Shape | Shape is the base class for all shape elements — for example, Line, Ellipse, Polygon, and Rectangle. |
| Control | Control derives from FrameworkElement and is the base class for all user-interactive elements. |
| ContentControl | ContentControl is the base class for all controls that have a single content (for example, Label, Button). The default style of a content control may be limited, but it is possible to change the look by using templates. |
| ItemsControl | ItemsControl is the base class for all controls that contain a collection of items content (for example, ListBox, ComboBox). |
| Panel | The class Panel derives from FrameworkElement and is the abstract base class for all panels. This class has a Children property for all UI elements within the panel and defines methods for arranging the child controls. Classes that are derived from Panel define different behavior for how the children are organized — for example, WrapPanel, StackPanel, Canvas, and Grid. |

As you can see, WPF classes have a really deep hierarchy. In this and the next chapters, you see classes of the core functionality, but it is not possible to cover all the features of WPF in this book.

## SHAPES

Shapes are the core elements of WPF. With shapes you can draw 2-dimensional graphics using rectangles, lines, ellipses, paths, polygons, and polylines that are represented by classes derived from the abstract base class Shape. Shapes are defined in the namespace System.Windows.Shapes.

The following XAML example draws a yellow face consisting of an ellipse for the face, two ellipses for the eyes, two ellipses for the pupils in the eyes, and a path for the mouth:

```xml
<Window x:Class="ShapesDemo.MainWindow"
xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
Title="Window1" Height="300" Width="300">
<Canvas>
<Ellipse Canvas.Left="0" Canvas.Top="0" Width="100" Height="100" Stroke="Blue"
StrokeThickness="4" Fill="Yellow" />
<Ellipse Canvas.Left="30" Canvas.Top="12" Width="60" Height="30" >
```
