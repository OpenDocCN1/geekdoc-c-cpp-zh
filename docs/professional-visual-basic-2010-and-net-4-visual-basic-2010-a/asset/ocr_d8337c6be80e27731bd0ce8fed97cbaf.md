The new activity has three properties: the input text, a language pair that defines the source and target languages, and the output text (the latter being a read-only property). You can create properties normally in an activity, but it is beneficial to create them so that they participate in the workflow and are available to other activities. In order to do this, use the following pattern to describe your properties:

```
Public Shared SomeProperty As DependencyProperty = _
    DependencyProperty.Register("PropertyName", _
    GetType(ReturnType), _
    GetType(ClassName))
Public Property PropertyName () As ReturnType
    Get
        Return CType(MyBase.GetValue(SomeProperty), _
            ReturnType)
    End Get
    Set(ByVal value As ReturnType)
        MyBase.SetValue(SomeProperty, value)
    End Set
End Property
```

Code snippet from TranslateActivity

The initial shared field of type DependencyProperty identifies the field that will be used to communicate with other activities. DependencyProperty is a common type used in WF programming, enabling easier communication between nested types. The Public property enables the more common use of the property. Notice that it stores the data in the shared property between all instances of the type.

As described, there are three properties in the translate activity:

```
Public Shared InputTextProperty As DependencyProperty = _
    DependencyProperty.Register("InputText", _
    GetType(System.String), _
    GetType(TranslateActivity))
Public Shared TranslationTypeProperty As DependencyProperty = _
    DependencyProperty.Register("TranslationType", _
    GetType(TranslationOptions), _
    GetType(TranslateActivity))
Public Shared OutputTextProperty As DependencyProperty = _
    DependencyProperty.Register("OutputText", _
    GetType(System.String), _
    GetType(TranslateActivity))
<DesignerSerializationVisibility(DesignerSerializationVisibility.Visible)> _
<BrowsableAttribute(True)> _
<DescriptionAttribute("Text to be translated")> _
Public Property InputText() As String
    Get
        Return CStr(MyBase.GetValue(InputTextProperty))
    End Get
    Set(ByVal value As String)
        MyBase.SetValue(InputTextProperty, value)
    End Set
End Property
<DesignerSerializationVisibility(DesignerSerializationVisibility.Visible)> _
<BrowsableAttribute(False)> _
<DescriptionAttribute("Translated text")> _
Public ReadOnly Property OutputText() As String
    Get
        Return CStr(MyBase.GetValue(OutputTextProperty))
    End Get
End Property
<DesignerSerializationVisibility(DesignerSerializationVisibility.Visible)> _
<BrowsableAttribute(True)> _
<DescriptionAttribute("Language pair to use for the translation")> _
```