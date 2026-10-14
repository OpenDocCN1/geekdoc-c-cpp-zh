
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

The decorators for logging and transaction management are *cross-cutting concerns*. Irrespective of the method on the interface and, in many cases, irrespective of the interface itself, logging and transaction management could be applied. Thus, to avoid repetitive implementations for multiple interfaces, you can decorate all implementations by using aspect-oriented programming.

Some other decorators apply only to a subset of the methods of a single interface, rather than to all of them. For example, you might want to prompt the user before you permanently delete an entity from persistent storage—a common requirement. Remember that you do not want to edit an existing class, which would violate the open/closed principle. Instead, you should create a new implementation of an existing interface that clients are already using to perform the delete action. This is the Delete method of the ICreateReadUpdateDelete<TEntity> interface. Such an implementation would look like Listing 8-3.

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

The DeleteConfirmation<TEntity> class decorates only the Delete method, as its name suggests. The other methods are implemented with pass-through delegation to the wrapped interface. Pass-through means that there is no decoration for that method: the call is merely passed through the decorator to the underlying implementation, almost as if it had been called directly. Despite the fact that these pass-through methods apparently do nothing special, in order to maintain unit test coverage and ensure that they are delegating properly, test methods should still be written to verify that their behavior is correct. This is laborious when compared to the alternative: interface segregation.

By separating the Delete method from the rest of the ICreateReadUpdateDelete<TEntity> interface, you have two interfaces, as shown in Listing 8-4.

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

This allows the confirmation decorator to be replaced with an implementation only for the IDelete<TEntity> interface, as shown in Listing 8-5.

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

This is an improvement, because there is less code overall, without the pass-through decoration methods, so the intent is much clearer. Also, less code means less testing.

Before moving on to the next decorator, consider the following refactor that is available for the DeleteConfirmation decorator. You should encapsulate the user interrogation into a simple interface. This way, you could write multiple different implementations of this new interface—one for each user interface type (for example, console, Windows Forms, and Windows Presentation Foundation)—and the decorator would not need to change. You should do this because the DeleteConfirmation class does not currently adhere to the single responsibility principle. As it is now, it contains two reasons to change: the interface that it delegates to has changed, and you want to elicit confirmation from the user in a different manner. Asking users whether they want to delete an entity requires a very simple predicate-like interface, as shown in Listing 8-6.

## LISTING 8-6 A very simple interface for asking the user to confirm something.

Click here to view code image

```
public interface IUserInteraction
{
    bool Confirm(string message);
}
```

## Caching

The next decorator that you could implement is for the read methods: ReadOne and ReadAll. For both of these methods, you want to cache the returned value from the decorated implementation and return the contents of the cache in all subsequent requests. Again, with no equivalent analogy for caching the Create or Update methods, the first decorator contains needless methods, as in Listing 8-7.

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
