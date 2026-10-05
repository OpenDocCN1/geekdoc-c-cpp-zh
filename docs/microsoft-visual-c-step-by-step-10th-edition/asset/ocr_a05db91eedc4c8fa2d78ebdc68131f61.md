```
class BigDisposableType : IDisposable, IAsyncDisposable
{
    private bool disposed = false;
    ...
    public void Dispose()
    {
        if (!this.disposed)
        {
            // Perform synchronous disposal logic
            ...
        }
        this.disposed = true;
        GC.SuppressFinalize(this);
    }

    public async ValueTask DisposeAsync()
    {
        await this.DisposeAsyncCore();
        this.Dispose();
    }

    private Task DisposeAsyncCore()
    {
        // Dispose of large objects asynchronously
        ...
    }
}
```