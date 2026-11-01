If you want to set metadata for a property, then you must use an object that derives from `PropertyMetadata`, such as `FrameworkPropertyMetadata`, and pass this instance as the fourth parameter to `Register()`. There are 11 overloads of the `FrameworkPropertyMetadata` constructor, and they take one or more of the parameters shown in Table 15-5.

# TABLE 15-5: Overloads for the FrameworkPropertyMetadata Constructor

| PARAMETER TYPE | USAGE |
|---|---|
| object defaultValue | The default value for the property. |
| FrameworkPropertyMetadataOptions flags | A combination of the flags from the FrameworkPropertyMetadataOptions enum) that you can use to specify additional metadata for a property. For example, you might use AffectsArrange to declare that changes to the property might affect control layout. This would cause the layout engine for a window to recalculate control layout if the property changed. See the MSDN documentation for a full list of the options available here. |
| PropertyChangedCallback propertyChangedCallback | The callback method to use when the property value changes. |
| CoerceValueCallback coerceValueCallback | The callback method to use if the property value is coerced. |
| bool isAnimationProhibited | Specifies whether this property can be changed by an animation. |
| UpdateSourceTrigger defaultUpdateSourceTrigger | When property values are data-bound, this property determines when the data source is updated, according to values in the UpdateSourceTrigger enum. The default value is PropertyChanged, which means that the binding source is updated as soon as the property changes. This is not always appropriate — for example, the TextBox.Text property uses a value of LostFocus for this property. This ensures that the binding source is not updated prematurely. You can also use the value Explicit to specify that the binding source should be updated only when requested (by calling the UpdateSource() method of a class derived from DependencyObject). |

A simple example of using `FrameworkPropertyMetadata` is to use it to set the default value of a property: