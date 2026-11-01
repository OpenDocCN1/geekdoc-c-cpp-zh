Support cancellation by accepting a `CancellationToken` parameter in async methods to allow consumers to cancel long-running operations.

```
```csharp
public async Task<int> ProcessDataAsync(int id,
CancellationToken cancellationToken = default)
{
    await Task.Delay(1000, cancellationToken); // Simulated
long-running operation
    return id;
}
```
```

# 7. Avoid Blocking Calls:

Avoid blocking calls like `Task.Result`, `Task.Wait`, or synchronous APIs within async methods, as they can lead to deadlocks and degrade performance.

```
```csharp
public async Task<int> GetDataAsync(int id)
{
    // Avoid blocking calls like Task.Result or synchronous APIs
here
    await Task.Delay(100); // Simulated async operation
    return id * 10;
}
```
```

# 8. Use Async Initialization:

For types that require asynchronous initialization, use async constructors or factory methods to initialize asynchronously.

```
```csharp
public class DataService
{
    private readonly HttpClient _httpClient;
```
```