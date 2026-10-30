The IEvent interface is extremely simple, containing just a string Name property. By using these two interfaces, a decorator can be created, as in Listing 10-13, that publishes a specific event when an entity is deleted.

# LISTING 10-13 This decorator publishes an event when an entity is deleted.

```
public class DeleteEventPublishing<TEntity> : IDelete<TEntity>
{
    private readonly IDelete<TEntity> decorated;
    private readonly IEventPublisher eventPublisher;

    public DeleteEventPublishing(IDelete<TEntity> decorated, IEventPublisher eventPublisher)
    {
        this.decorated = decorated;
        this.eventPublisher = eventPublisher;
    }

    public void Delete(TEntity entity)
    {
        decorated.Delete(entity);
        var entityDeleted = new EntityDeletedEvent<TEntity>(entity);
        eventPublisher.Publish(entityDeleted);
    }
    // ...
    public class EntityDeletedEvent<TEntity> : IEvent<TEntity>
    {
        public EntityDeletedEvent(TEntity entity) : base("EntityDeleted")
        {
            DeletedEntity = entity;
        }

        public TEntity DeletedEntity
        {
            get;
            private set;
        }
    }
}
```

From here, you have two choices: implementing the equivalent ISave decorator for publishing events on the same class or implementing the ISave decorator in a new class. Listing 10-14 shows the former option, which involves renaming the existing class and adding a new Save method.