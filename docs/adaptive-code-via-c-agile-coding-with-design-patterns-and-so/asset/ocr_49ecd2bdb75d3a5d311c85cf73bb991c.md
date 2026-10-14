```
```csharp
public interface IRead<TEntity>
{
    TEntity ReadOne(Guid identity);

    IEnumerable<TEntity> ReadAll();
}
// ...
public class ReadCaching<TEntity> : IRead<TEntity>
{
    private TEntity cachedEntity;
    private IEnumerable<TEntity> allCachedEntities;

    private readonly IRead<TEntity> decorated;
    public ReadCaching(IRead<TEntity> decorated)
    {
        this.decorated = decorated;
    }

    public TEntity ReadOne(Guid identity)
    {
        if(cachedEntity == null)
        {
            cachedEntity = decorated.ReadOne(identity);
        }
        return cachedEntity;
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
```