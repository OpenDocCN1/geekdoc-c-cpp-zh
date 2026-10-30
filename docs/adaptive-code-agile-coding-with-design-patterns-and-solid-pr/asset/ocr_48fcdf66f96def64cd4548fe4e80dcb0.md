persistent storage for an entity. Figure 10-1 shows a UML class diagram explaining the operations available to the ICreateReadUpdateDelete interface.

![](bbox=[0.124, 0.11, 0.354, 0.224])

**FIGURE 10-1** The initial interface before segregation.

The read operations are split into two methods, one for retrieving a single record from storage and another for reading all records. In code, this interface is as shown in Listing 10-1.

```
**LISTING 10-1** A simple interface for CRUD operations on an entity.

```csharp
public interface ICreateReadUpdateDelete<TEntity>
{
    void Create(TEntity entity);

    TEntity ReadOne(Guid identity);

    IEnumerable<TEntity> ReadAll();

    void Update(TEntity entity);

    void Delete(TEntity entity);
}
```
```

The ICreateReadUpdateDelete interface is generic, allowing reuse across different entity types. However, by making the interface generic, rather than making each individual method generic, you force clients to declare up front which TEntity you are dealing with, which clarifies dependencies. If a client wants to perform CRUD operations on more than one entity, it must request multiple ICreateReadUpdateDelete<TEntity> instances, one for each entity type.

> **Note** Though clients will require an *instance* of `ICreateReadUpdateDelete<TEntity>` per entity type, there could still only be one *implementation* of `ICreateReadUpdateDelete<TEntity>` that would suffice for all concrete entity types. Such an implementation would also be generic.

Every operation of CRUD is performed by each implementation of the ICreateReadUpdateDelete interface—including any decorator. This would be acceptable for decorators such as logging or transaction handling, as Listing 10-2 shows.