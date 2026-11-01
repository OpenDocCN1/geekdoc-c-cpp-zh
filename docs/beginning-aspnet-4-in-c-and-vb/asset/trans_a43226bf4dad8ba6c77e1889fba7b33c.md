

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

代码片段 BooksDemo/BooksModel.Designer.cs

下表解释了与实体类相关的重要类和接口。除了 INotifyPropertyChanging 和 INotifyPropertyChanged 之外，这些类型都定义在命名空间 System.Data.Objects.DataClasses 中。

| 类或接口 | 描述 |
|---|---|
| StructuralObject | StructuralObject 是 EntityObject 和 ComplexObject 类的基类。此类实现了 INotifyPropertyChanging 和 INotifyPropertyChanged 接口。 |
| INotifyPropertyChanging<br>INotifyPropertyChanged | 这些接口定义了 PropertyChanging 和 PropertyChanged 事件，以便在对象状态发生变化时订阅相关信息。与此处的其他类和接口不同，这些接口定义在命名空间 System.ComponentModel 中。 |
| EntityObject | 此类派生自 StructuralObject，并实现 IEntityWithKey、IEntityWithChangeTracker 和 IEntityWithRelationships 接口。EntityObject 通常用作映射到包含键和与其他对象存在关系的数据库表的对象的基类。 |
| ComplexObject | 此类可用作不具有键的实体对象的基类。它派生自 StructuralObject，但不像 EntityObject 类那样实现其他接口。 |

| 类或接口 | 描述 |
|---|---|
| IEntityWithKey | 此接口定义了 EntityKey 属性，可用于快速访问对象。 |
| IEntityWithChangeTracker | 此接口定义了 SetChangeTracker() 方法，可将实现 IChangeTracker 接口的更改跟踪器分配给该方法，以获取对象的状态更改信息。 |
| IEntityWithRelationships | 此接口定义了只读属性 RelationshipManager，该属性返回一个 RelationshipManager 对象，可用于在对象之间进行导航。 |

> > 对于实体类而言，不必从基类 EntityObject 或 ComplexObject 派生。实体类也可以实现所需的接口。

通过使用对象上下文类 BooksEntities，可以轻松访问 Book 实体类。Books 属性返回一个 Book 对象集合，可以对其进行迭代：

```
using (var data = new BooksEntities())
{
    foreach (var book in data.Books)
    {
        Console.WriteLine('{0}, {1}', book.Title, book.Publisher);
    }
}
```

## 对象上下文

要从数据库中检索数据，需要使用 ObjectContext 类。此类定义了实体对象到数据库的映射。使用核心 ADO.NET 时，可以将此类与用于填充 DataSet 的数据适配器进行比较。

设计器创建的 BooksEntities 类派生自基类 ObjectContext。此类添加了用于传递连接字符串的构造函数。使用默认构造函数时，将从配置文件中读取连接字符串。也可以将已打开的连接以 EntityConnection 实例的形式传递给构造函数。如果向构造函数传递尚未打开的连接，则对象上下文会打开并关闭该连接；如果传递的是已打开的连接，则还需要关闭它。

创建的类定义了 Books 和 Authors 属性，这些属性返回 ObjectSet<TEntity>。ObjectSet<TEntity> 是 .NET 4 中新增的类型，并派生自 ObjectQuery<TEntity>：

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

代码片段 BooksDemo/BooksModel.Designer.cs

ObjectContext 类向调用方提供了多项服务：

- 它会跟踪已检索的实体对象。如果再次查询该对象，则会从对象上下文中获取它。
- 它会保留实体的状态信息。可以获取有关已添加、已修改和已删除对象的信息。
- 可以从对象上下文更新实体，以将更改写入基础存储。

下表列出了 ObjectContext 类的方法和属性。

| OBJECTCONTEXT 方法和属性 | 描述 |
|---|---|
| Connection | 返回与对象上下文关联的 DbConnection 对象。 |
| MetadataWorkspace | 返回可用于读取元数据和映射信息的 MetadataWorkspace 对象。 |
| QueryTimeout | 使用此属性可以获取和设置对象上下文查询的超时值。 |
| ObjectStateManager | 此属性返回一个 ObjectStateManager。ObjectStateManager 会跟踪对象上下文中检索到的实体对象和对象更改。 |

| OBJECTCONTEXT 方法和属性 | 描述 |
|---|---|
| CreateQuery() | 此方法返回一个 ObjectQuery，用于从存储中获取数据。前面所示的 Books 和 Authors 属性使用此方法返回 ObjectQuery。 |
| GetObjectByKey() TryGetObjectByKey() | 这些方法通过键从对象状态管理器或基础存储中返回对象。如果键不存在，GetObjectByKey() 会引发 ObjectNotFoundException 类型的异常。TryGetObjectByKey() 返回 false。 |
| AddObject() | 此方法将新的实体对象添加到对象上下文中。 |
| DeleteObject() | 此方法从对象上下文中删除对象。 |
| Detach() | 此方法将实体对象从对象上下文中分离，使其在发生更改时不再被跟踪。 |
| Attach() AttachTo() | Attach() 方法将分离的对象附加到存储中。要将对象重新附加到对象上下文，实体对象必须实现 IEntityWithKey 接口。AttachTo() 方法不要求对象具有键，但要求提供实体集名称，以确定实体对象应附加到的位置。 |
| ApplyPropertyChanges() | 如果对象已从对象上下文中分离，随后分离的对象被修改，并且之后需要将更改应用于对象上下文中的对象，则可以调用 ApplyPropertyChanges() 方法来应用更改。这在以下场景中非常有用：从 Web 服务返回一个分离的对象，在客户端对其进行更改，然后以修改后的形式将其传回 Web 服务。 |
| Refresh() | 当实体对象存储在对象上下文中时，存储中的数据可能会发生变化。可以使用 Refresh() 方法从存储中刷新数据。使用此方法时，可以传递一个 RefreshMode 枚举值。如果存储与对象上下文中的对象值不同，传递 ClientWins 值会更改存储中的数据；传递 StoreWins 值会更改对象上下文中的数据。 |
| SaveChanges() | 在对象上下文中添加、修改和删除对象不会更改基础存储中的对象。使用 SaveChanges() 方法将更改持久化到存储中。 |
| AcceptAllChanges() | 此方法将上下文中对象的状态更改为未修改。SaveChanges() 会隐式调用此方法。 |

## 关系

实体类型 Book 和 Author 彼此相关。一本书由一个或多个作者共同创作，而一位作者可以创作一本或多本书。关系基于相关类型的数量和多重性。ADO.NET Entity Framework 支持多种关系，其中一些关系如下所示，包括每个层次结构一个表（TPH）和每个类型一个表（TPT）。多重性可以是一对一、一对多或多对多。

## 每个层次结构一个表

使用 TPH 时，数据库中有一个表对应于实体类层次结构。Payments 数据库表（见图 31-3）包含实体类型层次结构的列。其中一些列对层次结构中的所有实体都是通用的，例如 Id 和 Amount。CreditCardNumber 列仅供信用卡付款使用。

![](img/d7d2ffa0a76feaab821930e95daace93_934_0.png)

