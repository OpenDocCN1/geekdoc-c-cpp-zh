# Field Template Interaction in Dynamic Forms

Is it possible to implement interaction between field templates in a dynamically generated web page? Yes. In fact you already have all the tools you need. Is it a good idea? Most of the time, it is not. When you discover that two or more data entry controls on a form need to interact with each other, the best course of action is to create a custom entity or page template, where implementing the interaction will be easier and more straightforward. Chapter 10, "Building Custom Forms," discusses how to accomplish this task in detail.

However, you might discover recurring patterns in your entity model, where different properties need the same type of interaction. In Chapter 10, a custom entity template was created for the Customer entity to help users enter address information by suggesting a list of regions based on the name of the country they entered. In the Northwind sample model, several other entities include address properties, including Customer, Employee, Supplier, and Order. After implementing the same pattern several times for different entities, you might decide that a single, dynamic implementation would be beneficial.

> **NOTE**
> 
> Remember that falling into the trap of creating a dynamic solution where custom code would be more appropriate is very common. Dynamic is not better than Custom. Don’t try to implement a dynamic solution based on just one or two instances of a particular pattern. With such a small number of cases, you will not have a sufficient understanding of the pattern and will not recoup the additional effort required to implement a dynamic solution. Even such a common pattern as the Region/Country properties could have been efficiently implemented with custom code, such as the generic Address entity template discussed in Chapter 4.

The key to implementing field template interaction with metadata is to place the logic of how to interact in the field templates and storing the information of who to interact with in the metadata. As an example, the Region field template created in Chapter 10 can be modified to provide an auto-completion list for users based on the value in the Country field template. However, the country property can have different names in different entities—it is called ShipCountry in the Order entity—you do not want to hard-code it in the Region field template itself. Instead, the Country property name can be specified as a control parameter in the UIHintAttribute for the Region property, as shown in this code snippet:

```
[MetadataType(typeof(Metadata))]
partial class Employee
{
    private abstract class Metadata
    {
        [UIHint("Region", "WebForms", "CountryField", "Country")]
        public object Region { get; set; }
    }
}
```