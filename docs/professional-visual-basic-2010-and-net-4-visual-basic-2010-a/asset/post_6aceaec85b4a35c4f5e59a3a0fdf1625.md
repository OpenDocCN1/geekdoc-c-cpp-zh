
+   - A set of text boxes to hold a name, address, and phone number, with the combined information formatted and validated in a particular way
+   - A set of option buttons with a single property exposed as the chosen option

As with inherited controls, composite controls are only appropriate for situations that require the same functionality in multiple places. If the functionality is only needed once, then simply placing the relevant controls on the form and including appropriate logic right in the form is usually better.

Composite controls in Windows Forms are most often created using the UserControl class as a base class. Composite controls can be created using other classes as a base, however, and a later section entitled Embedding Controls in Other Controls shows an example.

## Writing a Control from Scratch

If a control needs special functionality not available in any existing control, then it can be written from scratch to draw its own visual interface and implement its own logic. This option requires more work, but it enables you to do just about anything within .NET and Windows Forms, including very sophisticated user interfaces.

To write a control from scratch, it is necessary to inherit from the Control class, which provides basic functionality such as properties for colors and size. With this basic functionality already built in, your required development tasks include adding any specific properties and methods needed for the control, writing rendering logic that will paint the control to the screen, and handling mouse and keyboard input to the control.

## INHERITING FROM AN EXISTING CONTROL

With this background on the options for creating custom controls, the next step is to look in depth at the procedures used for their development. First up is creating a custom control by inheriting from an existing control and extending it with new functionality. This is the simplest method for the creation of new controls, and the best way to introduce generic techniques that apply to all custom controls.

After you look at the general steps needed to create a custom control via inheritance, an example illustrates the details. It is important to understand that many of the techniques described for working with a control created through inheritance also apply to the other ways that a control can be created. Whether inheriting from the Control class, the UserControl class, or from an existing control, a control is a .NET class. Creating properties, methods, and events, and coordinating these members with the Visual Studio designers, is done in a similar fashion, regardless of the starting point.

### Process Overview

Here are the general stages involved in creating a custom control via inheritance from an existing control. This is not a step-by-step recipe, just an overview. A subsequent example provides more detail on the specific steps, but those steps follow these basic stages:

+   1. Create or open a Windows Control Library project and add a new custom control to the project. The class that is created will inherit from the `System.Windows.Forms.Control` base class. The line that specifies the inherited class must be changed to inherit from the control that is being used as the starting point.
+   2. The class file gets new logic added as necessary to add new functionality. Then the project is compiled with a Build operation in order to create a DLL containing the new control’s code.
+   3. The control is now ready to be used. It can be placed in the Windows Forms Toolbox with the Choose Items option in Visual Studio 2010. From that point forward, it can be dragged onto forms like any other control.

Stage 2, of course, is where the effort lies. New logic for the custom control may include new properties, methods, and events. It may also include intercepting events for the base control and taking special actions as necessary. These tasks are done with standard .NET coding techniques.

Several coding techniques are specific to developing Windows Forms controls, such as using particular .NET attributes. While our example includes adding routine properties and events, we focus on these special techniques for programming controls.

### Writing Code for an Inherited Control

This section discusses how to place new logic in an inherited control, with special emphasis on techniques that go beyond basic object orientation. A detailed example using the techniques follows this section.

### Creating a Property for a Custom Control

Creating a property for a custom control is just like creating a property for any other class. It is necessary to write a property procedure, and to store the value for the property somewhere, most often in a module-level variable, which is often called a backing field.

Properties typically need a default value — that is, a value the property takes on automatically when the control is instantiated. Typically, this means setting the backing field that holds the property value to some initial value. That can be done when the backing field is declared, or it can be done in the constructor for the control.

Here’s the code for a typical simple property for a custom control:

```
Dim _nMaxItemsSelected As Integer = 10
Public Property MaxItemsSelected() As Integer
    Get
        Return _nMaxItemsSelected
    End Get
    Set(ByVal Value As Integer)
        If Value < 0 Then
            Throw New ArgumentException("property value cannot be negative")
        Else
            _nMaxItemsSelected = Value
        End If
    End Set
End Property
```

Code snippet from LimitedCheckedListBox

After a property is created for a control, it automatically shows up in the Properties window for the control. If your Properties window is arranged alphabetically, you will see it in the list. If your window is arranged by category, then the new property will appear in the Misc category. However, you can use some additional capabilities to make the property work better with the designers and the Properties window in Visual Studio.

### Coordinating with the Visual Studio IDE

Controls are normally dragged onto a visual design surface, which is managed by the Visual Studio IDE. In order for your control to work effectively with the IDE, it must be able to indicate the default value of its properties. The IDE needs the default value of a property for two important capabilities:

+   To reset the value of the property (done when a user right-clicks the property in the Properties window and selects Reset)
+   To determine whether to set the property in designer-generated code. A property that is at its default value does not need to be explicitly set in the designer-generated code.

There are two ways for your control to work with the IDE to accomplish these tasks. For properties that take simple values, such as integers, Booleans, floating-point numbers, or strings, .NET provides an attribute. For properties that take complex types, such as structures, enumerated types, or object references, two methods need to be implemented.

### Attributes

You can learn more about attributes in Chapter 4, but a short summary of important points is included here. Attributes reside in namespaces, just as components do. The attributes used in this chapter are in the `System.ComponentModel` namespace. To use attributes, the project must have a reference to the assembly containing the namespace for the attributes. For `System.ComponentModel`, that’s no problem — the project automatically has the reference.

However, the project will not automatically have an Imports statement for that namespace. Attributes could be referred to with a full type name, but that’s a bit clumsy. To make it easy to refer to the attributes in code, put the following line at the beginning of all modules that need to use the attributes discussed in this chapter:

```
Imports System.ComponentModel
```

That way, an attribute can be referred to with just its name. For example, the `DefaultValue` attribute, discussed in detail below, can be declared like this:

```
<DefaultValue(4)> Public Property MyProperty() As Integer
```

> All the examples in this chapter assume that the Imports statement has been placed at the top of the class, so all attributes are referenced by their short name. If you get a compile error on an attribute, then it’s likely that you’ve omitted that line.

Unlike earlier versions of Visual Basic, Visual Basic 2010 allows such lines of code to be split into separate lines, without the need for line continuation characters. For example, the last example could also be written as follows:

```
<DefaultValue(4)>
Public Property MyProperty() As Integer
```

### Setting a Default Value with an Attribute

The .NET Framework contains many attributes. Most are used to tag classes, properties, and methods with metadata — that is, information that some other entity, such as a compiler or the Visual Studio IDE, might need to know.

For example, the `DefaultValue` attribute tells the Visual Studio IDE the default value of a property. You can change the preceding code for a simple property to include a `DefaultValue` attribute. Here are the first few lines, showing the change to the property declaration that applies the attribute:

```
Dim mnMaxItemsSelected As Integer = 10
<DefaultValue(10)> Public Property MaxItemsSelected() As Integer
    Get
        Return mnMaxItemsSelected
    ...
```

Code snippet from LimitedCheckedListBox

Including the `DefaultValue` attribute enables the Properties window to reset the value of the property back to the default value. That is, if you right-click the property in the Properties window and select Reset from the pop-up context menu, the value of the property returns to 10 from any other value to which it was set.

Another effect of the attribute can be seen in the code generated by the visual designer. If the preceding property is set to any value that is not the default, a line of code appears in the designer-generated code to set the property value. This is called *serializing* the property.
