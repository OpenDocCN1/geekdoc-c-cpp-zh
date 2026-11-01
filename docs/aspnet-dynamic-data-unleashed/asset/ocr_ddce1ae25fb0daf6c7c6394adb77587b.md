Thanks to the power of LINQ to Objects, the UnleashedTableProvider constructor packs quite a bit of logic in just a few lines of code. Breaking it down into steps...the first part, shown next, uses the static TypeDescriptor class to obtain a list of PropertyDescriptor objects that represent custom properties of the entity class:

```
```csharp
IEnumerable<PropertyDescriptor> customProperties = TypeDescriptor
.GetProperties(original.EntityType).Cast<PropertyDescriptor>()
.Where(p => p.PropertyType.IsSubclassOf(typeof(EntityReference)))
.Where(p => this.RootEntityType.IsAssignableFrom(p.ComponentType))
.Where(p => original.Columns.All(c => c.Name != p.Name));
```
```

Several Where calls are used to filter out inapplicable properties. The first Where call eliminates the “reference” properties that Entity Framework generates for every foreign key property, such as the SupplierReference property, which accompanies the Supplier property. Whereas the Supplier property returns an object of type Supplier, the SupplierReference property returns an EntityReference<Supplier> that for the purpose of filtering represents the same logical metadata column. The second Where call removes the properties declared in the EntityObject base class or higher in the inheritance hierarchy of the entity class, such as the EntityKey property. The last Where call removes all entity properties already recognized by the original table provider:

```
```csharp
this.columns = original.Columns
.Concat(customProperties.Select(p => new UnleashedColumnProvider(this, p)))
.ToList().AsReadOnly();
```
```

Having obtained PropertyDescriptor objects, the second part of the UnleashedTableProvider constructor creates an UnleashedColumnProvider object for each custom property and “concatenates” them with the collection of ColumnProvider objects returned by the original TableProvider. Stored in the private columns field, this combined collection is returned by the Columns property overridden in this class.

To recap, the UnleashedTableProvider class implements the Decorator pattern and extends the list of columns returned by the original table provider to include the UnleashedColumnProvider objects for custom properties defined in the entity class. All other properties and methods overridden in the UnleashedTableProvider call the original implementation, reusing and preserving the built-in logic.

# Extending the DataModelProvider to Support Custom Properties

The UnleashedModelProvider inherits from the built-in DataModelProvider and encapsulates metadata information describing one or more entity classes. Each DataModelProvider is responsible for creating and returning a collection of TableProvider objects. Just like the MetaModel class discussed earlier in this chapter, you must subclass the DataModelProvider whenever you subclass the TableProvider.

The UnleashedModelProvider also implements the Decorator pattern by wrapping an original DataModelProvider instance. The main purpose of this class is to change the Tables