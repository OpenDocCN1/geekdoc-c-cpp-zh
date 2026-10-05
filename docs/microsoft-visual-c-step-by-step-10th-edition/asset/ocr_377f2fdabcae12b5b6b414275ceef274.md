```
public async Task<int> FindValueAsync(string key)
{
    bool foundLocally = GetCachedValue(key, out int result);
    if (foundLocally)
        return result;

    result = await RetrieveValue(key); // possibly takes a long time
    AddItemToLocalCache(key, result);
    return result;
}
```