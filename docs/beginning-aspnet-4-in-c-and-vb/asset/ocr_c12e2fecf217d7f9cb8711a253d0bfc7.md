ScaffoldAllTables property of the ContextConfiguration for the sites to true, as illustrated in this code for the LINQ to SQL site:

```
```
DefaultModel.RegisterContext(typeof(MagicShopDataContext),
    new ContextConfiguration() { ScaffoldAllTables = true });
```
```

code snippet PCSDynamicDataDemoLinq/Global.asax

If the value is changed to false, then the default behavior is not to provide any scaffolding for any tables or columns. In order to instruct the dynamic data framework to scaffold a table of column, you must provide metadata in your data model. This metadata will then be read by the dynamic data runtime, and scaffolding will be generated for you. Metadata can also provide information for other things — such as validation logic — as you will see shortly.

To supply metadata for a table, you must do two things:

+   - Create a metadata class definition for each table you want to supply metadata for, with members that map to columns.
+   - Associate the metadata classes with the data model table classes.

All data model items, in both LINQ to SQL and ADO.NET Entities, are generated for you as partial class definitions. In the sample code, for example, there is a class called Customer (contained in the MagicShopModel namespace in the ADO.NET Entities version) that is used for rows in the Customer table. To supply metadata for Customer rows, you might create a class called CustomerMetadata. Once you have done that, you can supply a second partial class definition for Customer and use the MetadataType attribute to link the classes together.

In the .NET Framework, metadata is supported through data annotations. As such it should come as no surprise that the MetadataType attribute, along with other metadata attributes, is found in the System.ComponentModel.DataAnnotations namespace. The MetadataType attribute uses a Type parameter to specify the metadata type. The two attributes that control scaffolding are ScaffoldTable and ScaffoldColumn. Both of these attributes have a Boolean parameter to specify whether scaffolding will be generated for a table or column.

The following code shows an example of how this is achieved:

```
```
using System.ComponentModel.DataAnnotations;

...

[MetadataType(typeof(CustomerMetadata))]
public partial class Customer { }
```
```

code snippets PCSDynamicDataDemoEntities/App_Code/Customer.cs and PCSDynamicDataDemoLinq/App_Code/Customer.cs

```
```
using System.ComponentModel.DataAnnotations;

...

[ScaffoldTable(true)]
public class CustomerMetadata
{
    [ScaffoldColumn(false)]
    public object Address { get; set; }
}
```
```

code snippets PCSDynamicDataDemoEntities/App_Code/CustomerMetadata.cs and PCSDynamicDataDemoLinq/App_Code/CustomerMetadata.cs

Here, the ScaffoldTable attribute specifies that scaffolding will be generated for the Customer table, and the ScaffoldColumn attribute is used to ensure that the Address column will have no scaffolding. Note