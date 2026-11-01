
```csharp
ReportPropertyChanging("Id");
_Id = StructuralObject.SetValidValue(value);
ReportPropertyChanged("Id");
OnIdChanged();
}
}
private int _Id;
partial void OnIdChanging(int value);
partial void OnIdChanged();
[EdmScalarPropertyAttribute(EntityKeyProperty=false, IsNullable=false)]
[DataMemberAttribute()]
public string Title
{
    get
    {
        return _Title;
    }
    set
    {
        OnTitleChanging(value);
        ReportPropertyChanging("Title");
        _Title = StructuralObject.SetValidValue(value, false);
        ReportPropertyChanged("Title");
        OnTitleChanged();
    }
}
private string _Title;
partial void OnTitleChanging(string value);
partial void OnTitleChanged();
[EdmScalarPropertyAttribute(EntityKeyProperty=false, IsNullable=false)]
[DataMemberAttribute()]
public string Publisher
{
    get
    {
        return _Publisher;
    }
    set
    {
        OnPublisherChanging(value);
        ReportPropertyChanging("Publisher");
        _Publisher = StructuralObject.SetValidValue(value, false);
        ReportPropertyChanged("Publisher");
        OnPublisherChanged();
    }
}
private string _Publisher;
partial void OnPublisherChanging(string value);
partial void OnPublisherChanged();
[EdmScalarPropertyAttribute(EntityKeyProperty=false, IsNullable=true)]
[DataMemberAttribute()]
public string Isbn
{
    get
    {
        return _Isbn;
    }
    set
    {
    OnIsbnChanging(value);
    ReportPropertyChanging("Isbn");
    _Isbn = StructuralObject.SetValidValue(value, true);
    ReportPropertyChanged("Isbn");
    OnIsbnChanged();
}
}
private string _Isbn;
partial void OnIsbnChanging(string value);
partial void OnIsbnChanged();

[XmlIgnoreAttribute()]
[SoapIgnoreAttribute()]
[DataMemberAttribute()]
[EdmRelationshipNavigationPropertyAttribute("BooksModel", "BooksAuthors", "Authors")]
public EntityCollection<Author> Authors
{
    get
    {
        return ((IEntityWithRelationships)this).RelationshipManager.
            GetRelatedCollection<Author>("BooksModel.BooksAuthors", "Authors");
    }
    set
    {
        if ((value != null))
        {
            ((IEntityWithRelationships)this).RelationshipManager.
                InitializeRelatedCollection<Author>("BooksModel.BooksAuthors",
                "Authors", value);
        }
    }
}
```

code snippet BooksDemo/BooksModel.Designer.cs

The classes and interfaces important in regard to entity classes are explained in the following table. With the exception of INotifyPropertyChanging and INotifyPropertyChanged, the types are defined in the namespace System.Data.Objects.DataClasses.

| CLASS OR INTERFACE | DESCRIPTION |
|---|---|
| StructuralObject | StructuralObject is the base class of the classes EntityObject and ComplexObject. This class implements the interfaces INotifyPropertyChanging and INotifyPropertyChanged. |
| INotifyPropertyChanging
INotifyPropertyChanged | These interfaces define the PropertyChanging and PropertyChanged events to allow subscribing to information when the state of the object changes. Different from the other classes and interfaces here, these interfaces are defined in the namespace System.ComponentModel. |
| EntityObject | This class derives from StructuralObject and implements the interfaces IEntityWithKey, IEntityWithChangeTracker, and IEntityWithRelationships. EntityObject is a commonly used base class for objects mapped to database tables that contain a key and relationships to other objects. |
| ComplexObject | This class can be used as a base class for entity objects that do not have a key. It derives from StructuralObject but does not implement other interfaces as the EntityObject class does. |

| CLASS OR INTERFACE | DESCRIPTION |
|---|---|
| IEntityWithKey | This interface defines an EntityKey property that allows fast access to the object. |
| IEntityWithChangeTracker | This interface defines the method SetChangeTracker() where a change tracker that implements the interface IChangeTracker can be assigned to get information about state change from the object. |
| IEntityWithRelationships | This interface defines the read-only property RelationshipManager, which returns a RelationshipManager object that can be used to navigate between objects. |

> > For an entity class, it's not necessary to derive from the base classes EntityObject or ComplexObject. Instead, an entity class can implement the required interfaces.

The Book entity class can easily be accessed by using the object context class BooksEntities. The Books property returns a collection of Book objects that can be iterated:

```
using (var data = new BooksEntities())
{
    foreach (var book in data.Books)
    {
        Console.WriteLine('{0}, {1}', book.Title, book.Publisher);
    }
}
```

## OBJECT CONTEXT

To retrieve data from the database, the ObjectContext class is needed. This class defines the mapping from the entity objects to the database. With core ADO.NET, you can compare this class to the data adapter that fills a DataSet.

The BooksEntities class created by the designer derives from the base class ObjectContext. This class adds constructors to pass a connection string. With the default constructor, the connection string is read from the configuration file. It is also possible to pass an already opened connection to the constructor in the form of an EntityConnection instance. If you pass a connection to the constructor that is not opened, the object context opens and closes the connection; if you pass an opened connection you also need to close it.

The created class defines Books and Authors properties, which return an ObjectSet<TEntity>. ObjectSet<TEntity> that is new with .NET 4 and derives from ObjectQuery<TEntity>:

```
public partial class BooksEntities : ObjectContext
{
    public BooksEntities() : base("name=BooksEntities", "BooksEntities")
    {
        this.ContextOptions.LazyLoadingEnabled = true;
        OnContextCreated();
    }

    public BooksEntities(string connectionString) : base(connectionString, "BooksEntities")
    {
        this.ContextOptions.LazyLoadingEnabled = true;
        OnContextCreated();
    }
}
```

```
public BooksEntities(EntityConnection connection) : base(connection, "BooksEntities")
{
    this.ContextOptions.LazyLoadingEnabled = true;
    OnContextCreated();
}

partial void OnContextCreated();

public ObjectSet<Author> Authors
{
    get
    {
        if ((_Authors == null))
        {
            _Authors = base.CreateObjectSet<Author>("Authors");
        }
        return _Authors;
    }
}
private ObjectSet<Author> _Authors;

public ObjectSet<Book> Books
{
    get
    {
        if ((_Books == null))
        {
            _Books = base.CreateObjectSet<Book>("Books");
        }
        return _Books;
    }
}
private ObjectSet<Book> _Books;
```

code snippet BooksDemo/BooksModel.Designer.cs

The ObjectContext class provides several services to the caller:

- It keeps track of entity objects that are already retrieved. If the object is queried again, it is taken from the object context.
- It keeps state information about the entities. You can get information about added, modified, and deleted objects.
- You can update the entities from the object context to write the changes to the underlying store.

Methods and properties of the ObjectContext class are listed in the following table.

| OBJECTCONTEXT METHODS AND PROPERTIES | DESCRIPTION |
|---|---|
| Connection | Returns a DbConnection object that is associated with the object context. |
| MetadataWorkspace | Returns a MetadataWorkspace object that can be used to read the metadata and mapping information. |
| QueryTimeout | With this property you can get and set the timeout value for the queries of the object context. |
| ObjectStateManager | This property returns an ObjectStateManager. The ObjectStateManager keeps track of entity objects retrieved and object changes in the object context. |

| OBJECTCONTEXT METHODS AND PROPERTIES | DESCRIPTION |
|---|---|
| CreateQuery() | This method returns an ObjectQuery to get data from the store. The Books and Authors properties shown earlier use this method to return an ObjectQuery. |
| GetObjectByKey() TryGetObjectByKey() | These methods return the object by the key either from the object state manager or the underlying store. GetObjectByKey() throws an exception of type ObjectNotFoundException if the key does not exist. TryGetObjectByKey() returns false. |
| AddObject() | This method adds a new entity object to the object context. |
| DeleteObject() | This method deletes an object from the object context. |
| Detach() | This method detaches an entity object from the object context, so it is no longer tracked if changes occur. |
| Attach() AttachTo() | The Attach() method attaches a detached object to the store. Attaching objects back to the object context requires that the entity object implements the interface IEntityWithKey. The AttachTo() method does not have the requirement for a key with the object, but it requires the entity set name where the entity object needs to be attached. |
| ApplyPropertyChanges() | If an object was detached from the object context, then the detached object is modified, and afterward the changes should be applied to the object within the object context, you can invoke the ApplyPropertyChanges() method to apply the changes. This is useful in a scenario where a detached object was returned from a Web service, changed from a client, and passed to the Web service in a modified way. |
| Refresh() | The data in the store can change while entity objects are stored inside the object context. To make a refresh from the store, the Refresh() method can be used. With this method you can pass a RefreshMode enumeration value. If the values for the objects are not the same between the store and the object context, passing the value ClientWins changes the data in the store. The value StoreWins changes the data in the object context. |
| SaveChanges() | Adding, modifying, and deleting objects from the object context does not change the object from the underlying store. Use the SaveChanges() method to persist the changes to the store. |
| AcceptAllChanges() | This method changes the state of the objects in the context to unmodified. SaveChanges() invokes this method implicitly. |

## RELATIONSHIPS

The entity types Book and Author are related to each other. A book is written by one or more authors, and an author can write one or more books. Relationships are based on the count of types they relate and the multiplicity. The ADO.NET Entity Framework supports several kinds of relationships, some of which are shown here, including Table-per-Hierarchy (TPH) and Table-per-Type (TPT). Multiplicity can be one-to-one, one-to-many, or many-to-many.

## Table per Hierarchy

With TPH, there's one table in the database that corresponds to a hierarchy of entity classes. The database table Payments (see Figure 31-3) contains columns for a hierarchy of entity types. Some of the columns are common to all entities in the hierarchy, such as Id and Amount. The CreditCardNumber column is only used by a credit card payment.

![](img/d7d2ffa0a76feaab821930e95daace93_934_0.png)
