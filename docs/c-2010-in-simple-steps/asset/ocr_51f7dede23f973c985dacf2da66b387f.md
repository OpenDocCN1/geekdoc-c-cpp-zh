# Namespaces and XAML

Similar to XML, XAML requires certain predefined namespaces to allow you to use elements and attributes in an XBAP application. Namespaces convey to the XAML parser the location of the classes and structural rules for a WPF application. When you create a standalone WPF application, references to the necessary namespaces are added in the Window element and the Page element (in XBAP applications) by default.

By default, two namespaces are included in WPF applications, as shown in Listing 7.1. The namespaces are added by using the xmlns attribute of the Window or Page element. The xmlns attribute is set as shown in the following code snippet:

```
xmlns=http://schemas.microsoft.com/winfx/2006/presentation
```

In the preceding code snippet, the xmlns attribute is set to the default namespace for the XAML code and WPF applications. This namespace is provided as a Uniform Resource Indicator (URI). The namespace includes all the XAML elements and attributes that are required to work with WPF.

The second xmlns attribute is set as shown in the following code snippet:

```
xmlns:x=http://schemas.microsoft.com/winfx/2006/xaml
```

In the preceding code snippet, the xmlns attribute is set to the namespace that is required to work with XAML in general. This namespace is more exhaustive than the default namespace as it provides all the essential XAML elements and attributes, including those that do not pertain to WPF, for example, the elements for WF and Silverlight.

Note that the second xmlns attribute (that refers to the XAML namespace) specifies x: as an alias for the namespace. This alias has to be prefixed with every element or attribute that belongs to the XAML namespace. For example, the x:Class attribute used in the Window element belongs to the XAML namespace and specifies the partial class (in the code-behind file) that implements the Window element, as shown in the following code snippet:

```
x:Class="wpfApplication1.MainWindow"
```

> Note
> You can add the xmlns attribute in any of the XAML elements. However, it is advisable to add the references in the root element of the XAML file, that is, the Window or Page element.

# Markup Extensions

Till now you learned to set properties of elements, such as buttons, by using string or numeric values directly and explicitly. However, in some cases, you may not want to directly set the properties to string or numeric values; rather, you may want the properties to be set to a reference to a particular object. For such situations, WPF offers markup extensions. A markup extension is a means of setting the value of a property to an object reference. It also allows you to delay the assignment of a value to a property until run time or to bind a property to a value.

Markup extensions provide an easy, flexible, and efficient way of assigning values to properties through attributes as well as the property element syntax. In WPF, markup extensions are offered by various markup extension classes that help you to set the property to different types of values. The markup extension classes inherit the System.Windows.Markup.MarkupExtension class. Table 7.1 lists some of the common markup extension classes:

Table 7.1: Common Markup Extension Classes

| Markup Extension Classes | XAML String Token | Description |
|---|---|---|
| BindingBase | Binding | Allows you to specify a data bound value for a given property |
| StaticResourceExtension | StaticResource | Allows you to specify an existing resource to determine the value of a property |