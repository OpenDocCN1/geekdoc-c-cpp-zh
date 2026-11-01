```
[MetadataType(typeof(Metadata))]
partial class Product
{
    private abstract class Metadata
    {
        [UIHint("Text", null, "Columns", 100)]
        [FilterUIHint("Text", null, "Columns", 100)]
        public object ProductName { get; set; }
    }
}
```

Just like the UnleashedControl, which was extended in Chapter 11 to automatically initialize matching public properties of the field templates based on the control parameters specified in the UIHintAttribute, the UnleashedFilter initializes public properties of the filter templates based on the information specified in the FilterUIHintAttribute, such as the Columns property in this example.

This chapter centers discussion on eliminating some of the shortcomings in Dynamic Data that make building metadata-driven list pages more difficult than they really need to be. It also continues the discussion of how to build list pages that display and allow searching information from multiple related entities, this time dynamically. To accomplish these goals, the sample solution extends the metadata information, which was reviewed in Chapter 7, “Metadata API.”

# Extending Filter Lookup Rules

As you might recall from a discussion in Chapter 3, “Field Templates,” Dynamic Data uses a sophisticated algorithm to locate field templates based on the metadata information describing entity properties. It first checks the entity property for presence of the UIHintAttribute, which can specify the name of a field template explicitly. If the property does not have a UI hint, Dynamic Data then checks it for the DataTypeAttribute, which can specify a business-level name of the property type, such as EmailAddress or Date, and look for field templates with the matching name. In the absence of a high-level data type, Dynamic Data uses a low-level type of the entity property, such as String or DateTime, to look for the matching field template. If a direct match is not immediately available, Dynamic Data uses a fallback algorithm to try more and more generic types, such as going from Float to decimal to string.

The lookup algorithm used for field templates makes it easier to develop dynamic pages because it significantly reduces the amount of additional data annotation attributes needed in the entity model. Unfortunately, Dynamic Data does not implement the same fallback-based rules for locating filter templates. In fact, it hard-codes the lookup rules to the three types of filter templates that come out of the box—Boolean, Enumeration, and ForeignKey. For all other types of properties—String, Int32, DateTime, and so on—the filter template name has to be specified explicitly.