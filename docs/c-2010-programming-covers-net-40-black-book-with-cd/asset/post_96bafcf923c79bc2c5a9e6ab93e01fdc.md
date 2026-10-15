
Although setting the properties through XAML attributes is easy, concise, and intuitive, WPF provides an alternate way, known as the property element syntax, to do so. In the property element syntax, you can set the properties by specifying them as elements rather than as attributes. In the property element syntax, the property is set by using the following syntax:

```
<element_name.property_name [attribute1_name="value1" attribute2_name="value2"...
attributeN_name="valueN"]>property_value</element_name.property_name>
```

In the preceding syntax, the following are the options used while setting a property:

- element_name – Specifies the name of the element to which the property belongs
- property_name – Specifies the name of the property
- attribute1_name, attribute2_name, ... attributeN_name – Specifies the name of any attributes that the property may contain
- value1, value2,... valueN – Specifies the values of the attributes
- property_value – Specifies the value of the property

As you can see from the preceding syntax, the property name is qualified with the element name to which it belongs by using the dot operator (.). You may also notice that the property is enclosed within angled brackets and has starting and closing tags. Note that if the property itself has its own properties, then those can further be represented in the property element syntax.

The following code snippet shows the properties of the Button class:

```
<Button>
  <Button.Height>23</Button.Height>
  <Button.Name>button1</Button.Name>
  <Button.Content>Welcome</Button.Content>
</Button>
```

In the preceding code snippet, the Height, Name, and Content properties are set by using the property element syntax. These properties are specified as XAML elements and the child elements of the Button element. In this and many other cases of WPF controls, the Content property replaces the Text property that is present in Windows Forms applications.

At this point, you may wonder as to whether to set the properties as attributes or elements. Note that both the approaches result in the same output. However, in situations where you want the XAML code to be clear and concise, you can set the properties as attributes. On the other hand, if you have properties that are complex object types, such as enumerations, then you can employ the property element syntax, which results in longer XAML code.

> **NOTE**
> In WPF, the values of properties can be any object of any type and not necessarily a string type that are enclosed within double quotes. For non-string values that are assigned to properties, the XAML parser automatically performs a type conversion, which is performed by type converters that are instances of the TypeConverter class. Note that not all of the properties have support for type conversion and for such properties setting improper values may result in an error. You can use the property element syntax to prevent any erroneous execution.

## Markup Extensions

Till now, WPF properties are set by using direct and explicit values. However, in some cases, you may not want to set the properties to string or numeric values, rather you may want the properties to be set to a reference to a particular object. For such situations, WPF offers markup extensions. A markup extension is a means of setting the value of a property to an object reference. It also allows you to delay the assignment of a value to a property until the runtime or bind a property to some value.

Markup extensions provide an easier, flexible, and efficient way of assigning values to properties through attributes as well as property element syntax. In WPF, there are several markup extension classes that assist you to set the property to different types of values. The markup extension classes inherit the System.Windows.Markup.MarkupExtension class and extend different types of markup extensions. Table 9.8 lists the different markup extension classes that are available in XAML:

## Table 9.8: Markup Extension Classes in XAML

| Markup Extension Class | Description |
|---|---|
| BindingBase | Allows you to specify a data bound value for a given property. |
| TemplateBindingExtension | Allows you to specify the property value of a control, which is specified to its control template. |
| StaticResourceExtension | Allows you to specify an existing resource that helps in determining the value of a property. |
| DynamicResourceExtension | Allows you to set the property value by delaying the reference to a given resource till runtime. |
| RelativeSource | Allows you to specify a relative source for binding the property. In other words, it specifies the location of the binding source with respect to the binding target. |
| ArrayExtension | Allows you to create arrays of XAML objects. |
| NullExtension | Allows you to set a null value to a property. |
| StaticExtension | Allows you to specify a static data member as the value of a property. |
| TypeExtension | Allows you to specify a Type object for the specified data type. |

## NOTE

> The markup extension classes are suffixed with the word, Extension. For instance, StaticResourceExtension is the name of a markup extension class. The word Extension is omitted when you use the markup extension class to set the values of properties. In addition, the markup extension classes that are prefixed with x: belong to the XAML namespace and those that are not prefixed with x: exist in the default WPF namespace.

As stated earlier, the markup extension classes are derived from the MarkupExtension class, which contains the ProvideValue() method. This method is responsible for returning the object that is to be assigned to the property after the evaluation of the markup extension. The object that is returned by the ProvideValue() method depends on the input that you provide to the markup extension. The input is passed on to a parameterized, non-default constructor of the markup extension class.

Markup extensions are characterized by their syntax that is very different from rest of the XAML content. You can provide a markup extension as either attributes or property elements. If you want to provide a markup extension as an attribute, then you need to enclose it within the curly braces ({ }). The opening curly brace is followed by the string token for the markup extension class. The string token is followed by a whitespace, which is then followed by input to the markup extension. Consider the following code snippet:

```
<Button Margin="100" Name="button1" Content="welcome" Style="{StaticResource mybackground}"/>
```

In the preceding code snippet, the StaticResource markup extension is used in the Button element to set the value for its Style property. When the markup extension is evaluated, mybackground is passed on to the non-default constructor of the StaticResourceExtension class.

If you want to provide a markup extension as a property element, then it is to be enclosed within angular brackets (< >) just as any other XAML element. The markup extension becomes the child element of the property. You will learn more about the individual markup extensions later in this book.

Let’s explore WPF properties in the next section.

## WPF Properties

Earlier in this chapter, you have learned in brief about the properties of WPF and how they are implemented through XAML attributes and elements. Properties hold great significance in WPF as they are easy-to-use and easy-to-validate. The WPF classes and the XAML elements have a comprehensive collection of properties that you can use to manipulate the classes and elements. In addition to traditional CLR properties, WPF includes dependency and attached properties.

## Dependency Properties

You gained a brief insight into the DependencyObject and DependencyProperty classes earlier in this chapter. These classes play a key role in the WPF property system. The WPF property system allows you to extend the existing CLR properties by backing them as dependency properties. Dependency properties are specific to WPF and refer to those properties that depend on various factors or inputs, such as data binding, animations, resources, and styles to determine their values. Most of the WPF properties are dependency properties as they support many of the complex and advanced functionalities.

There are various dependency properties offered by the WPF classes. The dependency properties can be categorized as follows:

- Read-only Dependency Property – Refers to a dependency property that is read-only and cannot be modified. Read-only dependency properties are useful in cases where you want the value of a dependency property to be set only once. You may also use a read-only dependency property when you want that its value is influenced by only one input and not others.
- Collection-type Dependency Property – Refers to a dependency property, which has a value of a collection type.

All dependency properties are instances of the DependencyProperty class. This class backs a CLR property by allowing you to create its objects and registering them with the WPF property system. The DependencyProperty class contains several properties and methods that assist you in implementing and working with dependency properties in WPF. Table 9.9 lists the noteworthy properties of the DependencyProperty class:

Table 9.9: Noteworthy Properties of the DependencyProperty Class

| Property | Description |
|---|---|
| DefaultMetadata | Retrieves the default metadata of a particular dependency property. |
| GlobalIndex | Retrieves the index that uniquely identifies a dependency property. The index is created and assigned automatically. |
| Name | Retrieves the name of a particular dependency property. |
| OwnerType | Retrieves the type of the object in which a given dependency property is created and registered. |
| PropertyType | Retrieves the type of the value of a given dependency property. |
| ReadOnly | Allows you to specify whether a dependency property is read-only. |
| ValidateValueCallback | Retrieves the name of the validation callback for a particular dependency property. |

Table 9.10 lists the noteworthy methods of the DependencyProperty class:

Table 9.10: Noteworthy Methods of the DependencyProperty Class

| Method | Description |
|---|---|
| AddOwner | Allows you to add another owner of an existing dependency property |
| GetMetadata | Retrieves the metadata of a particular dependency property |
| IsValidType | Allows you to check if the given value is acceptable as per the type of the dependency property or any of its derived types |
| IsValidValue | Allows you to check if the given value is acceptable as per the type of the dependency property and also lies in the acceptable range of values |
| OverrideMetadata | Allows you to provide a substitute metadata when the dependency property exists for another type |
| Register | Allows you to register a dependency property with the WPF property system |
