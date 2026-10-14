

interface—including any decorator. This would be acceptable for decorators such as logging or transaction handling, as Listing 8-2 shows.

## LISTING 8-2 Some decorators apply to all methods.

Click here to view code image

```
public class CrudLogging<TEntity> : ICreateReadUpdateDelete<TEntity>
{
    private readonly ICreateReadUpdateDelete<TEntity> decoratedCrud;
    private readonly ILog log;
    public CrudLogging(ICreateReadUpdateDelete<TEntity> decoratedCrud, ILog log)
    {
        this.decoratedCrud = decoratedCrud;
        this.log = log;
    }

    public void Create(TEntity entity)
    {
        log.InfoFormat("Creating entity of type {0}", typeof(TEntity).Name);
        decoratedCrud.Create(entity);
    }

    public TEntity ReadOne(Guid identity)
    {
        log.InfoFormat("Reading entity of type {0} with identity {1}", typeof(TEntity).Name, identity);
        return decoratedCrud.ReadOne(identity);
    }

    public IEnumerable<TEntity> ReadAll()
    {
        log.InfoFormat("Reading all entities of type {0}", typeof(TEntity).Name);
        return decoratedCrud.ReadAll();
    }

    public void Update(TEntity entity)
    {
        log.InfoFormat("Updating entity of type {0}", typeof(TEntity).Name);
        decoratedCrud.Update(entity);
    }

    public void Delete(TEntity entity)
    {
        log.InfoFormat("Deleting entity of type {0}", typeof(TEntity).Name);
        decoratedCrud.Delete(entity);
    }
}
//...
public class CrudTransactional<TEntity> : ICreateReadUpdateDelete<TEntity>
{
    private readonly ICreateReadUpdateDelete<TEntity> decoratedCrud;
    public CrudTransactional(ICreateReadUpdateDelete<TEntity> decoratedCrud)
    {
        this.decoratedCrud = decoratedCrud;
    }

    public void Create(TEntity entity)
    {
        using (var transaction = new TransactionScope())
        {
            decoratedCrud.Create(entity);

            transaction.Complete();
        }
    }

    public TEntity ReadOne(Guid identity)
    {
        TEntity entity;
        using (var transaction = new TransactionScope())
        {
            entity = decoratedCrud.ReadOne(identity);

            transaction.Complete();
        }
        return entity;
    }

    public IEnumerable<TEntity> ReadAll()
    {
        IEnumerable<TEntity> allEntities;
        using (var transaction = new TransactionScope())
        {
            allEntities = decoratedCrud.ReadAll();

            transaction.Complete();
        }
        return allEntities;
    }
}

public void Update(TEntity entity)
{
    using (var transaction = new TransactionScope())
    {
        decoratedCrud.Update(entity);

        transaction.Complete();
    }
}

public void Delete(TEntity entity)
{
    using (var transaction = new TransactionScope())
    {
        decoratedCrud.Delete(entity);

        transaction.Complete();
    }
}
```

用于记录和事务处理的装饰器是*横切关注点*。无论接口上的方法是什么，在许多情况下甚至无论接口本身是什么，记录和事务管理都可被应用。因此，为了避免为多个接口重复实现，您可以使用面向方面的编程来装饰所有实现。

有些装饰器仅适用于单个接口的方法子集，而不是全部。例如，您可能希望在从持久存储中永久删除实体之前提示用户——这是一个常见需求。请记住，您不希望编辑现有类，这会违反开闭原则。相反，您应该创建一个现有接口的新实现，客户端已在使用该接口来执行删除操作。这是 ICreateReadUpdateDelete<TEntity> 接口的 Delete 方法。这种实现看起来像 Listing 8-3。

## LISTING 8-3 If a decorator targets part of an interface, segregation is an option.

Click here to view code image

```
public class DeleteConfirmation<TEntity> : ICrud<TEntity>
{
    private readonly ICreateReadUpdateDelete<TEntity> decoratedCrud;
    public DeleteConfirmation(ICreateReadUpdateDelete<TEntity> decoratedCrud)
    {
        this.decoratedCrud = decoratedCrud;
    }

    public void Create(TEntity entity)
    {
        decoratedCrud.Create(entity);
    }

    public TEntity ReadOne(Guid identity)
    {
        return decoratedCrud.ReadOne(identity);
    }

    public IEnumerable<TEntity> ReadAll()
    {
        return decoratedCrud.ReadAll();
    }

    public void Update(TEntity entity)
    {
        decoratedCrud.Update(entity);
    }

    public void Delete(TEntity entity)
    {
        Console.WriteLine("Are you sure you want to delete the entity? [y/N]");
        var keyInfo = Console.ReadKey();
        if (keyInfo.Key == ConsoleKey.Y)
        {
            decoratedCrud.Delete(entity);
        }
    }
}
```

DeleteConfirmation<TEntity> 类仅装饰 Delete 方法，正如其名称所示。其他方法通过直通委托实现到被包装的接口。直通意味着该方法没有装饰：调用只是通过装饰器传递给底层实现，几乎就像直接调用一样。尽管这些直通方法看似没有做任何特殊的事情，为了保持单元测试覆盖率并确保它们正确地进行委托，仍然应该编写测试方法来验证其行为是否正确。与接口隔离相比，这很繁琐。

通过将 Delete 方法从其余的 ICreateReadUpdateDelete<TEntity> 接口中分离出来，您将拥有两个接口，如 Listing 8-4 所示。

## LISTING 8-4 The ICreateReadUpdateDelete interface is split in two.

Click here to view code image

```
public interface ICreateReadUpdate<TEntity>
{
    void Create(TEntity entity);

    TEntity ReadOne(Guid identity);

    IEnumerable<TEntity> ReadAll();

    void Update(TEntity entity);
}
// ...
public interface IDelete<TEntity>
{
    void Delete(TEntity entity);
}
```

这使得确认装饰器可以被仅针对 IDelete<TEntity> 接口的实现所替代，如 Listing 8-5 所示。

## LISTING 8-5 The confirmation decorator is applied only to the interface to which it pertains.

Click here to view code image

```
public class DeleteConfirmation<TEntity> : IDelete<TEntity>
{
    private readonly IDelete<TEntity> decoratedDelete;

    public DeleteConfirmation(IDelete<TEntity> decoratedDelete)
    {
        this.decoratedDelete = decoratedDelete;
    }

    public void Delete(TEntity entity)
    {
        Console.WriteLine("Are you sure you want to delete the entity? [y/N]");
        var keyInfo = Console.ReadKey();
        if (keyInfo.Key == ConsoleKey.Y)
        {
            decoratedDelete.Delete(entity);
        }
    }
}
```

这是一个改进，因为总体代码更少，没有了直通装饰方法，因此意图更加清晰。此外，代码更少意味着测试更少。

在继续下一个装饰器之前，请考虑对 DeleteConfirmation 装饰器可用的以下重构。您应该将用户询问封装到一个简单的接口中。这样，您可以为这个新接口编写多个不同的实现——每个用户界面类型一个（例如控制台、Windows 窗体和 Windows Presentation Foundation）——而装饰器无需更改。您应该这样做，因为 DeleteConfirmation 类目前不符合单一职责原则。如今，它有两个变更原因：它委托到的接口已更改，以及您希望以不同方式从用户那里获取确认。询问用户是否要删除实体需要一个非常简单的类似谓词的接口，如 Listing 8-6 所示。

## LISTING 8-6 A very simple interface for asking the user to confirm something.

Click here to view code image

```
public interface IUserInteraction
{
    bool Confirm(string message);
}
```

## Caching

您接下来可以实现的下一个装饰器是用于读取方法：ReadOne 和 ReadAll。对于这两种方法，您希望缓存来自被装饰实现返回的值，并在所有后续请求中返回缓存的内容。同样，对于 Create 或 Update 方法没有缓存的等效类比，第一个装饰器包含不必要的 pass-through 方法，如 Listing 8-7 所示。

## LISTING 8-7 The caching decorator includes redundant, pass-through methods.

Click here to view code image

```
public class CrudCaching<TEntity> : ICreateReadUpdate<TEntity>
{
    private TEntity cachedEntity;
    private IEnumerable<TEntity> allCachedEntities;
    private readonly ICreateReadUpdate<TEntity> decorated;

    public CrudCaching(ICreateReadUpdate<TEntity> decorated)
    {
        this.decorated = decorated;
    }
}
```

