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

# OBJECT CONTEXT

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