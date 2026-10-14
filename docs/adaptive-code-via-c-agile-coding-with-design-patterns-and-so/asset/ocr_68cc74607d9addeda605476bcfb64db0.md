![](bbox=[0.28, 0.01, 0.78, 0.27])

# FIGURE 8-1 The initial interface before segregation.

The read operations are split into two methods, one for retrieving a single record from storage and another for reading all of the records. In code, this interface is as shown in Listing 8-1.

# LISTING 8-1 A simple interface for CRUD operations on an entity.

Click here to view code image

```
public interface ICreateReadUpdateDelete<TEntity>
{
    void Create(TEntity entity);

    TEntity ReadOne(Guid identity);

    IEnumerable<TEntity> ReadAll();

    void Update(TEntity entity);

    void Delete(TEntity entity);
}
```

The ICreateReadUpdateDelete interface is generic, allowing reuse across different entity types. However, by making the interface generic, rather than making each individual method generic, you force clients to declare up front which TEntity you are dealing with, which clarifies its dependencies. If a client wants to perform CRUD operations on more than one entity, it will have to request multiple ICreateReadUpdateDelete<TEntity> instances, one for each entity type.

# Note

Though clients will require an instance of ICreateReadUpdateDelete<TEntity> per entity, there could still only be one implementation of ICreateReadUpdateDelete<TEntity> that would suffice for all concrete TEntity types. This implementation would also be generic.

Every operation of CRUD is performed by each implementation of the ICreateReadUpdate-Delete