```
```csharp
using System.Threading.Tasks;

public class Program
{
    public static async Task Main()
    {
        string filePath = "example.txt";
        try
        {
            string content = await ReadFileAsync(filePath);
            Console.WriteLine("File content:");
            Console.WriteLine(content);
        }
        catch (Exception ex)
        {
            Console.WriteLine("Error reading file: " + ex.Message);
        }
    }

    public static async Task<string> ReadFileAsync(string filePath)
    {
```
```