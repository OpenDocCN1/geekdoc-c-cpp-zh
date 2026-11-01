new row, ROWVERSION columns for which the server generates incremental values with every insert and update, as well as the computed columns defined at the database table level.

Dynamic Data always chooses a read-only field template to display values of generated columns, regardless of whether the entity itself is displayed in Insert or Edit mode.

```
```csharp
public bool IsCustomProperty { get; }
```
```

The IsCustomProperty of the MetaColumn class returns true for properties defined by developers in code as opposed to the normal properties defined in the data model itself. Out of the box, custom properties cannot be used for sorting or filtering purposes. The framework also cannot verify that they are persisted in the database correctly. Because of these reasons, Dynamic Data makes a safe bet and does not create filter or field controls for custom properties by default; although it is possible to change this behavior by applying UIHintAttribute and FilterUIHintAttribute to the property in code.

> > **NOTE**
> >
> > As of .NET version 4.0, service pack 1, the Dynamic Data provider for Entity Framework does not support custom properties, and you will not find MetaColumn objects describing them. This is why it is impossible to use custom properties as display columns. As mentioned earlier, this problem can be solved by extending the metadata provider, which is discussed in Chapter 13.

# Data Annotations

A large number of the MetaColumn public interface is dedicated to data annotations—the .NET attributes that can be applied by developers to the entity properties in code.

```
```csharp
public AttributeCollection Attributes { get; }
```
```

All attributes applied to a particular entity property can be accessed through the Attributes property of the MetaColumn class. Similar to the Attributes property of the MetaTable class, this property also includes the built-in attributes from the System.ComponentModel and System.ComponentModel.DataAnnotations namespaces as well as any custom attributes that you might have created in your application.

Although it is possible to get all data annotations directly through the Attributes collection, doing so would require scanning it repeatedly, which would quickly drain the precious CPU resources of your web server. Instead, Dynamic Data class scans the attributes only once, when the MetaColumn object is created, and stores their values in fields of the object for instantaneous access later.

# Scaffolding Support

Several data annotations and MetaColumn properties play an important role in the scaffolding process, where Dynamic Data determines whether a particular column needs to be