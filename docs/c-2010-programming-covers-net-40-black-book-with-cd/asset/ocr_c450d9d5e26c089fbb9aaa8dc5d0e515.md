In the preceding syntax:

+   - private, static, void, DependencyObject, DependencyPropertyChangedEventArgs – Represents the C# keywords
+   - propertyChangedMethod – Represents the name of the method that is passed as an argument to the PropertyChangedCallback delegate
+   - dObject – Represents the owner of the dependency property

> NOTE
> The coerce value and property changed callbacks belong to the property metadata; however, the validation callback is not contained in the property metadata.

Now, let’s discuss about dependency property metadata.

# Dependency Property Metadata

Every dependency property has a metadata that refers to an object containing a lot of information about the dependency property. The dependency property metadata can include the default value of the dependency property and reference to coerce and property changed callbacks. You can access the metadata to retrieve or change the information about the dependency property. The dependency property metadata is useful when you want to change the value of an existing dependency property without re-implementing the dependency property or creating a new dependency property. You can change or override the metadata of a dependency property in the derived classes of the owner of the dependency property.

The dependency property metadata is implemented through the PropertyMetadata class. The PropertyMetadata class has a derived class called UIPropertyMetadata, which itself is inherited by the FrameworkPropertyMetadata class. The FrameworkPropertyMetadata class is the class that is mainly used to work with the property metadata for the dependency properties. The FrameworkPropertyMetadata class has several Boolean properties that influence various metadata options of dependency properties. Table 9.12 lists some of the noteworthy properties of the FrameworkPropertyMetadata class:

| Table 9.12: Noteworthy Properties of the FrameworkPropertyMetadata Class |
| Property | Description |
| AffectsArrange | Allows you to specify if the dependency property influences the arrange pass of the element. The arrange pass of an element means how much space is provided to the element and ask it to fall into line. This property is of Boolean type and can be set to true or false. |
| AffectsMeasure | Allows you to specify if the dependency property influences the measure pass of the element. The measure pass of an element means to determine the space that the element needs to use for displaying purpose. This property is of Boolean type and can be set to true or false. |
| AffectsParentArrange | Allows you to specify if the dependency property influences the arrange pass of its parent element. This property is of Boolean type and can be set to true or false. |
| AffectsParentMeasure | Allows you to specify if the dependency property influences the measure pass of its parent element. This property is of Boolean type and can be set to true or false. |
| AffectsRender | Allows you to specify if the dependency property influences the rendering of elements. This property is of Boolean type and can be set to true or false. |
| BindsTwoWaysByDefault | Allows you to specify whether two-way data binding is the default binding for a dependency property. This property is of Boolean type and can be set to true or false. |
| CoerceValueCallback | Sets or retrieves the coerce value callback method that is used to coerce values on a dependency property. |