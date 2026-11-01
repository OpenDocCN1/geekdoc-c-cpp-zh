```
```csharp
public Expression Expression
{
    get { return this.GetQueryable().Expression; }
}

public Type ElementType
{
    get { return this.GetQueryable().ElementType; }
}

public IQueryProvider Provider
{
    get { return this.GetQueryable().Provider; }
}

public void AddObject(T entity)
{
    this.original.AddObject(entity);
}

public void Attach(T entity)
{
    this.original.Attach(entity);
}

public void DeleteObject(T entity)
{
    this.original.DeleteObject(entity);
}

public void Detach(T entity)
{
    this.original.Detach(entity);
}

private IQueryable GetQueryable()
{
    if (customQueryAttribute == null) return this.original;
    return customQueryAttribute.GetQueryable(this.original);
}
}
```
```