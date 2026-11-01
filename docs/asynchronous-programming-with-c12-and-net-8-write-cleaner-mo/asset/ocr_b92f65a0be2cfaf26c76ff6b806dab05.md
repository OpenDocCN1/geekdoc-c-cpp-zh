```
var response = await httpClient.GetAsync(url);
response.EnsureSuccessStatusCode();
// Read data asynchronously in chunks
var stream = await
response.Content.ReadAsStreamAsync();
using var reader = new
System.IO.StreamReader(stream);
while (!reader.EndOfStream)
{
    yield return await reader.ReadLineAsync();
}
}
async Task ProcessDataAsync()
{
    await foreach (var line in FetchDataAsync(apiUrl))
    {
        // Process each line asynchronously
        await Task.Delay(500); // Simulate processing delay
        Console.WriteLine($"Processed line: {line}");
    }
}
```