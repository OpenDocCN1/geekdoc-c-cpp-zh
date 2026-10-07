
Finally, the code uses the XpsDocumentWriter's Write method to write the document's paginator into the print queue.

Figure 17-6 shows the PrintFlowDocument program running in TwoPage, so it displays two pages of the FlowDocument's contents.

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_351_0.png)

FIGURE 17-6

The program displays its FlowDocument inside a FlowDocumentReader. Note that the format of the program's printout depends on the reader's mode when you make the printout. Figures 17-7 through 17-9 show the results when the reader is in Page mode, TwoPage mode, and Scroll mode, respectively.

Figures 17-7 and 17-8 look a lot like previous versions, although the printed results are smaller than they appear in the figures. The figures make it look like each page is fully full, but when printed, the results occupy only the upper third of the printed page.

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_351_1.png)

FIGURE 17-7

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_351_2.png)

FIGURE 17-8

Figure 17-9 looks almost exactly the same as the printed version.

As is the case with the previous examples, since the PrintDocument method tries to print all to the paper's upper-left corner, the top and left edges of the output are clipped unless you include margins within the FlowDocument.

You can get a more consistent result by setting the FlowDocument's PageHeight and PageWidth properties. Unfortunately, setting these properties appropriately for the printer makes the result on the screen small.

One way to work around this problem is to set the control's properties just before printing and restore their original values afterward.

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_352_0.png)

FIGURE 17-9

> BUG ALERT

Because of an apparent bug in the FlowDocumentReader, the control does not redraw properly after printing in Scroll mode. If you try to scroll the control after printing, it crashes.

If you change the control's zoom level or viewing mode, it refreshes itself, and all is well.

## FixedDocuments

The PrintFixedDocument example program in Figure 17-10 displays a FixedDocument inside a DocumentViewer control.

If the user clicks on the printer icon on the upper left, the viewer automatically launches a print dialog, and if the user selects a printer and clicks OK, it handles the printing for you.

If you want to do the work yourself, it's not hard to print a FixedDocument programmatically using the same code you would use to print a FlowDocument. Simply replace the

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_352_1.png)

FIGURE 17-10

FlowDocument with a FixedDocument. See the previous section for more information about printing FlowDocuments.

## SUMMARY

WPF's PrintDialog class provides easy access to the printing system. Its PrintVisual method lets you print a single page displaying an image of a visual control almost effortlessly. Its PrintDocument method lets you generate more complex printouts such as multi-page documents, FlowDocuments, and FixedDocuments.

Earlier chapters in this book explain how to set a control's properties to a value defined in a resource, style, or template. For example, if you define a string resource, you can later set a Window's Title property to the value of that resource.

This is a handy technique for centralizing and reusing values but it ignores other potentially useful data sources such as the properties of other controls and objects defined by code-behind.

The following chapter describes WPF data binding methods that let you attach a control's properties to objects other than resources including arrays of values, other controls' properties, and the properties of other kinds of objects.

# 18
# Data Binding

WPF data bindings lets you bind to a data source so the target automatically displays the value in the data source. For example, this lets you:

- Make a ListBox display an array of values defined in XAML code.
- Make a ListBox display a list of objects created in code-behind.
- Make a TreeView build a hierarchical display of objects created in code-behind.
- Make TextBoxes, Labels, and other controls display additional detail about the current-selected item in ListBox, ComboBox, or TreeView.

Additional WPF data-binding features let you sort, filter, and group data; let the user modify a control to update a data source; validate changes to data.

This chapter provides an introduction to data binding in WPF. It explains how bindings to associate objects and how to use bindings to let a control use values supplied by other controls, XAML resources, and objects created in code-behind.

## BINDING BASICS

Data bindings have these four basic pieces:

- Target — The object that will use the result of the binding
- Target Property — The target object's property that will use the result
- Source — The object that provides a value for the target object to use
- Path — A path that locates the value within the source object

As a trivial example, suppose you want to bind a Label's Content property so that the Label displays what you type in a TextBox. If the Label control is lblResult and the TextBox is named txtTypeHere, then you would need to create a binding where:

- The target is lblResult (the control where you want the binding's result to go).
- The Text property is Content (what you Label to display the result in its Content property).
- The source is txtType (the object providing the value).
- The path is txtPath (the path to the source object, in this case, the TextBox's property).

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_355_0.png)

The TextBoxToLabel example program in Figure 18-1 demonstrates this concept of simple binding. When you type in the text, the two labels enable whatever you type.

## Binding and Target Property

The target and target property are the easiest parts of binding to understand. The target is the control that contains the binding, and the target property is the property that is set to. In the following code, Label control is the target, and its Content property is the target property:

```xml
<Label Margin="5" BorderBrush="Yellow" BorderThickness="1"
       Content="Binding ElementName=txtType, Path=Text"/>
```

## It All Depends

A binding's target property must be a dependency property. Fortunately, most of the properties that you are most likely to bind are dependency properties.

The situation is somewhat confusing when the target uses several pieces of the data. For example, suppose you define a Planet class to track information about planets. Its properties include Name, Picture, Stats, and so forth.

If you make a collection of Planet objects, you can bind it to a ListBox that displays all of these values. This case is a bit more complicated than binding a Label's Content property to a TextBox's Text property.

The short explanation for this example is that the target property is the ListBox's ItemsSource property. The section "Binding Collections" later in this chapter explains how a ListBox can convert a bound to its ItemsSource property into a display of the collection's fields.

## Binding Source

The binding's source is the object from which it takes a value. This object can be a WPF control, XML data, or an object defined in the program's code-behind.

You can specify the source by setting any of the binding's ElementName, Source, or RelativeSource properties.

## Pick One

You can specify only one of the ElementName, Source, and RelativeSource properties at a time.

## ElementName

The binding's ElementName property gives the name of a control. The TextBoxToLabel example earlier uses ElementName to identify the TextBox that a binding should use as its source.

## Source

The binding's Source property identifies an object that should be used as a binding's source. Typically, a program uses a StaticResource to define this object.
