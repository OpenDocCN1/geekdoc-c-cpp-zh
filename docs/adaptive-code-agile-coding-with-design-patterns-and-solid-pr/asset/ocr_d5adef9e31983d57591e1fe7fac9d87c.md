```
public ReadCaching(IRead<TEntity> decorated)
{
    this.decorated = decorated;
}
public TEntity ReadOne(Guid identity)
{
    var foundEntity = cachedEntities [identity];
    if(foundEntity == null)
    {
        foundEntity = decorated.ReadOne(identity);
        if(foundEntity != null)
            cachedEntities [identity] = foundEntity;
    }
    return foundEntity;
}
public IEnumerable<TEntity> ReadAll()
{
    if (allCachedEntities == null)
    {
        allCachedEntities = decorated.ReadAll();
    }
    return allCachedEntities;
}
}
```

Before you implement the final decorator, the remaining interface contains only two methods, as Listing 10-9 shows.

# LISTING 10-9 The remaining methods can probably be unified.

```
public interface ICreateUpdate<TEntity>
{
    void Create(TEntity entity);
    void Update(TEntity entity);
}
```

The Create and Update methods have identical signatures. Not only that, they serve very similar purposes: the former saves a new entity, and the latter saves an existing entity. You could unify these methods into one Save method, which acknowledges that the distinction between creating and updating is an implementation detail that clients don’t need to know about. After all, a client is likely to want to both save and update an entity, so requiring two interfaces that are so similar seems needless when there is a viable alternative. Clients of the interface want to save an entity. The refactored interface looks like the one in Listing 10-10.