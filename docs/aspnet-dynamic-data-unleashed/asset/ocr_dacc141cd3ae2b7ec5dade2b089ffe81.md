FilterUIHintAttribute to the Country property of the Product entity class, as shown in the following example:

```
```csharp
partial class Product
{
    [UIHint("Parent", null, "DisplayField", "Country")]
    [FilterUIHint("Parent", null, "DisplayField", "Country")]
    public string Country { get { return this.Supplier.Country; } }
}
```
```

From the compiler standpoint, nothing prevents you from using the Parent field and filter templates this way; however, code in these templates currently assumes that they are associated with a foreign key property. Although Country, the custom property you created, uses the Supplier foreign key property internally, this information is not immediately available to the template. You can provide the missing information by passing an additional control parameter, ForeignKeyField, with the name of the foreign key property, as shown next:

```
```csharp
[UIHint("Parent", null,
    "ForeignKeyField", "Supplier",
    "DisplayField", "Country")]
[FilterUIHint("Parent", null,
    "ForeignKeyField", "Supplier",
    "DisplayField", "Country")]
public string Country { get { return this.Supplier.Country; } }
```
```

To take advantage of the new control parameter, the Parent templates need to be modified. The code snippet that follows shows how to extend the Parent field template to define a public property called ForeignKeyField, matching the name of the control parameter specified in the UIHintAttribute and replacing the ForeignKeyColumn property to locate the foreign key column based on its name. If the ForeignKeyField was not specified, the property falls back to the inherited implementation, which assumes that the template is associated with a foreign key property. The filter template can be extended in the same way; you can see its implementation in the source code that accompanies the book:

```
```csharp
public partial class ParentFieldTemplate : UnleashedFieldTemplate
{
    private MetaForeignKeyColumn foreignKeyColumn;

    public string ForeignKeyField { get; set; }

    public new MetaForeignKeyColumn ForeignKeyColumn
    {
        get
        {
            if (this.foreignKeyColumn == null)
            {
```
```