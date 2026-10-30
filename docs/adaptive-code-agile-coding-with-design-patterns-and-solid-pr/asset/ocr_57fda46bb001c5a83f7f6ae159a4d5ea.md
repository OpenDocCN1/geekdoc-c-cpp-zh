```
public void CreateEntity(TEntity entity)
{
    saver.Save(entity);
}

public TEntity GetSingleEntity(Guid identity)
{
    return reader.ReadOne(identity);
}

public void UpdateEntity(TEntity entity)
{
    saver.Save(entity);
}

public void DeleteEntity(TEntity entity)
{
    deleter.Delete(entity);
}
```

There is little difference between this version of the controller and the prior one, but the impact on the amount of code that you might have to write could be significant. This controller can be instantiated to operate on any entity, and the service interfaces that are required are all forced to agree on the same operation. No longer can you supply different types for each one—such as ISave<Customer>, IRead<Order>, IDelete<LineItem>.

Either version of the controller can be created in much the same way. Listing 10-17 shows how you must instantiate each class that implements the required interfaces before passing them in to the controller's constructor.

# LISTING 10-17 Creating the OrderController with separate instances of the dependencies.

```
static OrderController CreateSeparateServices()
{
    var reader = new Reader<Order>();
    var saver = new Saver<Order>();
    var deleter = new Deleter<Order>();

    return new OrderController(reader, saver, deleter);
}
```