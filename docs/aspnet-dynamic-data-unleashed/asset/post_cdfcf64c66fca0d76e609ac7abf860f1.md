
new row, ROWVERSION columns for which the server generates incremental values with every insert and update, as well as the computed columns defined at the database table level.

Dynamic Data always chooses a read-only field template to display values of generated columns, regardless of whether the entity itself is displayed in Insert or Edit mode.

```csharp
public bool IsCustomProperty { get; }
```

The IsCustomProperty of the MetaColumn class returns true for properties defined by developers in code as opposed to the normal properties defined in the data model itself. Out of the box, custom properties cannot be used for sorting or filtering purposes. The framework also cannot verify that they are persisted in the database correctly. Because of these reasons, Dynamic Data makes a safe bet and does not create filter or field controls for custom properties by default; although it is possible to change this behavior by applying UIHintAttribute and FilterUIHintAttribute to the property in code.

> **NOTE**
> 
> As of .NET version 4.0, service pack 1, the Dynamic Data provider for Entity Framework does not support custom properties, and you will not find MetaColumn objects describing them. This is why it is impossible to use custom properties as display columns. As mentioned earlier, this problem can be solved by extending the metadata provider, which is discussed in Chapter 13.

## Data Annotations

A large number of the MetaColumn public interface is dedicated to data annotations—the .NET attributes that can be applied by developers to the entity properties in code.

```csharp
public AttributeCollection Attributes { get; }
```

All attributes applied to a particular entity property can be accessed through the Attributes property of the MetaColumn class. Similar to the Attributes property of the MetaTable class, this property also includes the built-in attributes from the System.ComponentModel and System.ComponentModel.DataAnnotations namespaces as well as any custom attributes that you might have created in your application.

Although it is possible to get all data annotations directly through the Attributes collection, doing so would require scanning it repeatedly, which would quickly drain the precious CPU resources of your web server. Instead, Dynamic Data scans the attributes only once, when the MetaColumn object is created, and stores their values in fields of the object for instantaneous access later.

## Scaffolding Support

Several data annotations and MetaColumn properties play an important role in the scaffolding process, where Dynamic Data determines whether a particular column needs to be represented by a field or filter control on a page and how the template for that control is selected.

```csharp
public virtual bool Scaffold { get; set; }
```

The Scaffold property of the MetaColumn class determines whether Dynamic Data will generate a field template for the entity property it represents. By default, Scaffold returns false for automatically generated, custom, and primitive properties that are a part of a foreign key. You can change the default value of this property by applying the ScaffoldColumnAttribute or the DisplayAttribute with the AutoGenerateField property value specified.

```csharp
public virtual string UIHint { get; }
```

The UIHint property of the MetaColumn class returns the name of a field template that Dynamic Data tries first when generating a control for the entity property. The UIHint property returns a blank string unless you apply the UIHintAttribute to the entity property in code.

```csharp
public DataTypeAttribute DataTypeAttribute { get; }
```

The DataTypeAttribute property returns the DataTypeAttribute that was applied to the entity property in code. The UIHint and data type take precedence over the more generic template names based on .NET types that Dynamic Data tries when searching for an appropriate field template.

```csharp
public string FilterUIHint { get; }
```

The FilterUIHint property is similar to the UIHint but specifies the name of a filter template. It also returns a blank string by default and can be specified by applying the FilterUIHintAttribute to the entity property. Dynamic Data uses filter hints when generating filter controls, typically as part of a QueryableFilterRepeater in the List page template.

```csharp
public bool AllowInitialValue { get; }
```

The AllowInitialValue property of the MetaColumn determines whether the entity property can have a value entered in Insert mode. The AllowInitialValue returns false for generated and read-only properties. You can also override it by applying the EditableAttribute to the entity property with the AllowInitialValue value specified.

## Business Logic Support

Several properties of the MetaColumn class provide support for business logic based on data annotations. This number is surprisingly small, as it covers only three of the attributes discussed in Chapter 3, “Field Templates.”

```csharp
public object DefaultValue { get; }
```

The Description property of the MetaColumn class returns the description specified in code by applying the DescriptionAttribute to the entity property. The built-in field templates Dynamic Data provides do not currently utilize this property. However, you can easily modify them and use this property to generate a tooltip for the data controls in field templates.

## Formatting Options

The last remaining data annotation properties worth mentioning are the ones related to formatting options that can be specified by applying the DisplayFormatAttribute to the entity property. These properties are used by the DynamicControl and DynamicField controls to implement flexible and consistent formatting of field values.

```csharp
public string DataFormatString { get; }
```

The DataFormatString property returns a string that contains a .NET format string, such as "{0:C}", that will be used to convert field value to a string by calling the Format method of the String class. Although including the parameter number 0 might seem unnecessary, knowing that there is only one field value to format, it is required for the format string to work properly.

```csharp
public bool ApplyFormatInEditMode { get; }
```

The ApplyFormatInEditMode property determines whether Dynamic Data will use the DataFormatString not only in Read-only mode on List and Details pages, but also in Edit mode as well.

```csharp
public string NullDisplayText { get; }
```

The NullDisplayText property specifies the text Dynamic Data will display when the field value is null.

```csharp
public bool ConvertEmptyStringToNull { get; }
```

The ConvertEmptyStringToNull property determines whether NullDisplayText will be used for empty strings as well.

```csharp
public bool HtmlEncode { get; }
```

The HtmlEncode property determines whether any special characters that might be a part of the field value will be encoded using HTML escape sequences. This property is true by default, making the dynamically generated pages immune against HTML injection attacks. You should only consider changing it when your application allows users to enter formatted text in HTML form and perform thorough cleanup of the values entered by users to remove dangerous HTML tags, such as <script>, before saving them in the database.

## The MetaForeignKeyColumn Class

The MetaForeignKeyColumn class is a specialized descendant of the MetaColumn class that represents many-to-one and one-to-one navigation properties, such as the Supplier property of the Product entity in the Northwind data model. These “foreign key” columns in the Dynamic Data metadata API have additional attributes that you can access through this class.

```csharp
public MetaTable ParentTable { get; }
```

The ParentTable property returns a MetaTable object describing the parent entity referenced by the foreign key. In case of the Supplier property of the Product entity, the ParentTable property returns the MetaTable object describing the Supplier entity. This property serves an important role in implementing filtering and navigation functionality. In particular, it is used by the ForeignKey field and filter templates to retrieve the rows from the parent table for display in a drop-down list.

```csharp
public ReadOnlyCollection<string> ForeignKeyNames { get; }
```

The ForeignKeyNames property of the MetaForeignKeyColumn class returns a collection of the primitive entity properties that form the foreign key. For the Supplier property of the Product entity, this property returns a collection with a single column name—SupplierID. The collection returned by this property has multiple items only if the parent table has a compound primary key and the foreign key includes multiple primitive properties.

### Presentation Logic

The remaining properties and methods of the MetaForeignKeyColumn class provide support for implementing presentation logic in Dynamic Data applications.

```csharp
public bool IsPrimaryKeyInThisTable { get; }
```

The IsPrimaryKeyInThisTable property of the MetaForeignKeyColumn class returns true if any of the primitive components of the foreign key is a member of the primary key of the entity itself. For example, the Order_Detail entity in the Northwind data model has a compound primary key that consists of OrderID and ProductID properties. The Order navigation property is represented by a MetaForeignKeyColumn whose IsPrimaryKeyInThisTable returns true because OrderID is a part of the primary key of the Order_Detail entity.

> **NOTE**
> 
> Dynamic Data does not allow editing primary key values by default and uses the IsPrimaryKeyInThisTable property to display read-only field templates for foreign key columns that are a part of a primary key in Edit mode.

```csharp
public IList<object> GetForeignKeyValues(object row);
```
