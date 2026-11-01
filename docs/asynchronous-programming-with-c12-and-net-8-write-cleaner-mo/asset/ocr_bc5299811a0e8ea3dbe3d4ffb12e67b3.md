The HttpClient class in ASP.NET Core provides powerful features for making HTTP requests to external APIs or services asynchronously. Using async/await with HttpClient ensures that the application remains responsive while waiting for the HTTP response.

# **Example**: Making Asynchronous GET Request

```
```csharp
using System;
using System.Net.Http;
using System.Threading.Tasks;

public class Program
{
    private static readonly HttpClient httpClient = new
HttpClient();

    public static async Task Main()
    {
        string url =
"https://jsonplaceholder.typicode.com/posts/1";

        try
        {
            HttpResponseMessage response = await
httpClient.GetAsync(url);
            response.EnsureSuccessStatusCode(); // Ensure
success status code (2xx)

            string responseBody = await
response.Content.ReadAsStringAsync();
            Console.WriteLine("Response from API:");
            Console.WriteLine(responseBody);
        }
        catch (Exception ex)
        {

```