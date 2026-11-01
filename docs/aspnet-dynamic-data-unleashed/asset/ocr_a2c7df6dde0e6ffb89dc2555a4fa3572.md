# Overriding Default Field Templates

Dynamic Data chooses an appropriate field template for each property based on its type. If you find yourself in a situation where you need to change the field template Dynamic Data selected, it is best to stop and ask yourself if the property has an appropriate type. For instance, if you have a string property and want to force Dynamic Data to use an integer field template, there is a good chance that the property type is incorrect. The best course of action in that situation would be to correct the problem at the source—in the entity model and the database.

If the property does have an appropriate type, but the .NET type is not specific enough for your needs, your next choice is to apply the DataTypeAttribute to the property in the metadata class. For example, the HomePhone property of the Employee entity is of type string; however, it is very different from another string property, Notes. The first stores phone numbers; the second stores one or more lines of text. Here is how you can clarify this distinction in the entity model by applying the DataTypeAttribute:

```
[MetadataType(typeof(Metadata))]
partial class Employee
{
    private abstract class Metadata
    {
        [DataType(DataType.PhoneNumber)]
        public object HomePhone { get; set; }

        [DataType(DataType.MultilineText)]
        public object Notes { get; set; }
    }
}
```

By applying the DataTypeAttribute, you are giving Dynamic Data a more specific type it can use to choose a more appropriate field template, such as the MultilineText_Edit field template that comes with Dynamic Data out of the box and the PhoneNumber_Edit field template created in Chapter 3, “Field Templates.”

> NOTE
> 
> Applying the DataTypeAttribute to specify MultilineText type for a string property should not be necessary in many circumstances. Dynamic Data is smart enough to automatically recognize properties mapped to database columns of type VARCHAR(MAX) or TEXT as MultilineText. Therefore, treat it with suspicion and remember that it is better to address a mismatch by changing the entity model instead of applying a data annotation attribute.