```
public class Program
{
    private static async Task WriteWebRequestSizeAsync(
        string url)
    {
        try
        {
            WebRequest webRequest =
                WebRequest.Create(url);
            WebResponse response =
                await webRequest.GetResponseAsync();
            using (StreamReader reader =
                new StreamReader(
                    response.GetResponseStream()))
            {
                string text =
                    await reader.ReadToEndAsync();
                Console.WriteLine(
                    FormatBytes(text.Length));
            }
        }
        catch (WebException)
        {
            // ...
        }
        catch (IOException )
        {
            // ...
        }
        catch (NotSupportedException )
        {
            // ...
        }
    }

    public static void Main(string[] args)
    {
        string url = "http://www.IntelliTect.com";
        if (args.Length > 0)
        {
            url = args[0];
        }

        Console.Write(url);

        Task task = WriteWebRequestSizeAsync(url);

        while (!task.Wait(100))
        {
            Console.Write(".");
        }

        // ...
    }
}
```