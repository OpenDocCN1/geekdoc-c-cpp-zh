Adding a multivalue converter as a resource in XAML is done the same way as for a single-value converter, however using it as part of a binding is different. Rather than using a simple binding, as you have been doing, you need to use a MultiBinding instead. A MultiBinding enables you to bind a property of the target to a list of source properties and get back a single value. Because a MultiBinding is made up of individual Binding elements, each binding can have their own converters if necessary.

Listing 18.6 shows how to use the PhotoSizeConverter in XAML.

# ## LISTING 18.6 Using a Multivalue Converter

```
<Label1> <Label.Content> <MultiBinding Converter="{StaticResource PhotoSizeConverterRef erence}"> <Binding Path="Metadata.Width"/> <Binding Path="Metadata.Height"/> </MultiBinding> </Label.Content> </Label>
```

The order in which the individual Binding elements appear in the MultiBinding is the order those values are stored in the array passed to the Convert method.

Converters, whether they are single or multivalue, are culture-aware. The Convert and ConvertBack methods both have a culture parameter that can be used to change the conversion based on cultural information.

The Convert and ConvertBack methods also have a parameter named parameter, which can be used to change the conversion. This parameter enables the flexibility of using a single converter that can produce different formats based on the value of the converter parameter argument.

# ### The ConverterParameter Property

> The ConverterParameter property of a MultiBinding is not a DependencyProperty, so you can't bind it. If you need an IMultiValueConverter to behave differently based on the value of some other source property, you need to find an alternative way of providing that value. One simple option is to include that value as the last binding element in the list.

# **Watch Out!**

For example, if you were to create a NameConverter for use in the AddressBook application that can display a contact's first and last names in different formats, based on the DisplayAsStyle enumeration, the XAML might look like Listing 18.7.