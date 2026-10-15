You can now access these dependency properties as CLR properties in the XAML or the code-behind file.

> NOTE
> If you want to reset the value of a dependency property, then you can use the ClearValue() method. With this method, it is not necessary that the dependency property changes back to the default value specified in the property metadata. In fact, the value to which the dependency property reverts is dependent on the inputs available at that time.

Let’s move on to learn about a particular kind of dependency property known as attached properties.

# Attached Properties

An attached property refers to a dependency property that you can access and set to any of the child objects or elements. The attached properties help the child elements to provide information about their appearance and presentation to the parent element. The attached properties of an element are available to all its child elements and each child element can set different values for the same attached property.

Note that attached properties are implemented as dependency properties in the parent or owning element and accessible in both XAML and code-behind file. However, except for certain situations in style triggers, you cannot retrieve the value of attached properties in XAML. Unlike rest of the dependency properties, attached properties are not wrapped within a CLR property as they have to be accessible to all the elements (the parent as well as the child elements). Such elements should be able to assign different values. Some examples of the attached properties include the Row and Column properties of the Grid element.

You can also create user-defined attached properties. To do so, the parent or owning element needs to inherit the DependencyObject class unless the attached property is available only for other elements and not the parent element. A field of the DependencyProperty type is declared to create the attached property, which is then registered using the RegisterAttached() method. You also need to implement the get and set accessors for the property through two static methods. The syntax for the get accessor method of attached properties is as follows:

```
public static type GetPropertyName (type target) {
    //return statement
}
```

In the preceding syntax:

+   - public, static—Represents the C# keywords.

+   - type—Represents a valid type.

+   - GetPropertyName—Represents the name of the method that implements the get accessor method of the attached property. Note that PropertyName in GetPropertyName signifies the actual name of the attached property; therefore, the method name varies on the basis of properties name. For example, if the name an attached property is, Center; then the static method implementing its get accessor is named as GetCenter.

+   - target—Represents the object or element that gets the value of the attached property.

Note that the get accessor of attached properties needs to have a return statement.

The syntax for the set accessor of attached properties is as follows:

```
public static type SetPropertyName( type target, type value) {
    //statements
}
```

In the preceding syntax:

+   - public, static—Represents the C# keywords

+   - type—Represents a valid type

+   - SetPropertyName—Represents the name of the method that implements the set accessor of the attached property. Note that PropertyName in SetPropertyName signifies the actual name of the attached property; therefore, the method name varies on the basis of properties name. For example, if the attached property is named Center, then the static method implementing its set accessor is named SetCenter.

+   - target—Represents the object or element on which the attached property is to be set.

+   - value—Represents the value that is to be set on the attached property.