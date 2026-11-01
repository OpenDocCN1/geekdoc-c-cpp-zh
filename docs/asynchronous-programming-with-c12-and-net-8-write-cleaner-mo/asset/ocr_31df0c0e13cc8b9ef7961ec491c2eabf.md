```
if (ClickedAsync != null)
    {
        await ClickedAsync();
    }
}
}
public class Program
{
    public static async Task Main()
    {
        var button = new Button();
        button.ClickedAsync += async () =>
        {
            await Task.Delay(1000); // Simulate asynchronous
operation
            Console.WriteLine("Button clicked asynchronously");
        };
        await button.OnClickAsync();
    }
}

```