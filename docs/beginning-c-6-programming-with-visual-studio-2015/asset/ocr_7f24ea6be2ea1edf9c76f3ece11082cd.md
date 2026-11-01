you close them properly. When an element in placed inside another in XAML, this element becomes the content of the enclosing element, meaning that the Button could also have been written like this:

```
<Button HorizontalAlignment="Left"
Margin="220,151,0,0"
VerticalAlignment="Top"
Width="75"
    Hello World
</Button>
```

Here, the Content property of the Button has been removed and the text is now a child node of the Button control. Content can be just about anything in XAML, which is also demonstrated in this example: The Button element is the content of the Grid element, which is itself the content of the Window element.

Most, if not all, controls can have content, and there are very few limits to what you can do to change the appearance of the built-in controls. Chapter 15 explores this in more detail.

# Namespaces

The Window element of the previous example is the root element of the XAML file. This element usually includes a number of namespace declarations. By default, the Visual Studio designer includes two namespaces that you should be aware of: http://schemas.microsoft.com/winfx/2006/xaml/presentation and http://schemas.microsoft.com/winfx/2006/xaml. The first one is the default namespace of WPF and declares a lot of controls that you are going to use to create user interfaces. The second one declares the XAML language itself. Namespaces don't have to be declared on the root tag, but doing so ensures that their content can be easily accessed throughout the XAML file, so there is rarely any need to move the declarations.

> NOTE The namespaces looks like they might be URLs, but this is deceiving. In fact they are what is known as Uniform Resource Identifiers (URIs). A URI can be any string as long as it uniquely identifies a resource. Microsoft has chosen to specify the URLs in a form that is normally used for URLs, but in this case you will not get a result if you type them into your browser.

When you create a new window in Visual Studio, the presentation namespace is always declared as the default and the language namespace as xmlns:x. As seen with the Window, Button, and Grid tags, this ensures that you don't have to prefix the controls you add to the window, but the language elements you specify must be prefixed with an x.

The last namespace that you will see quite often is the system namespace: xmlns:sys="clr-namespace:System;assembly=mscorlib". This namespace allows you to use the built-in types of the .NET Framework in your XAML. By doing this, the markup you write can explicitly declare the types of elements you are creating. For example, it is possible to declare an array in markup and state that the members of the array are strings:

```
<Window.Resources>
<ResourceDictionary>
```