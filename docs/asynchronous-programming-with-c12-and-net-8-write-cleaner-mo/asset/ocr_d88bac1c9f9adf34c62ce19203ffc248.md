```
{
    try
    {
        using var httpClient = new HttpClient();
        var response = await httpClient.GetAsync(url);
        response.EnsureSuccessStatusCode();
        return await response.Content.ReadAsStringAsync();
    }
    catch (HttpRequestException ex)
    {
        Console.WriteLine($"Error fetching data:
{ex.Message}");
        throw; // Re-throw the exception
    }
}
async Task ProcessDataAsync(string data)
{
    try
    {
        // Simulate data processing asynchronously
        await Task.Delay(1000); // Simulate 1 second delay
```