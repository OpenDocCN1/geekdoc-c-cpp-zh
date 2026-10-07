

# 286 第 5 章：参数与方法

```csharp
if (is null) throw new ArgumentNullException(...)
```

你可以使用空合并赋值运算符配合 `throw ArgumentNullException` 表达式，在参数值为空时在单条语句中完成此操作（参见列表 5.32）。

列表 5.32：通过抛出 ArgumentNullException 进行参数验证

```csharp
httpsUrl = httpsUrl ??
throw new ArgumentNullException(nameof(httpsUrl));
fileName = fileName??
throw new ArgumentNullException(nameof(fileName));
```

```csharp
// ...
```

在 .NET 7.0 中，你可以使用 `ArgumentNullException.ThrowIfNull()` 方法（参见列表 5.33）。

列表 5.33：使用 ArgumentNullException.ThrowIfNull 进行参数验证

```csharp
ArgumentNullException.ThrowIfNull(httpsUrl);
ArgumentNullException.ThrowIfNull(fileName);
```

```csharp
// ...
```

在内部，`ArgumentNullException.ThrowIfNull()` 方法也会抛出 `ArgumentNullException`。

> 指南
> 务必验证非空引用类型参数是否为空，如果是，则抛出 ArgumentNullException。
> 务必在 .NET 7.0 或更高版本中使用 ArgumentNullException.ThrowIfNull() 来验证值是否为空。

# 使用异常进行基础错误处理 287

# 额外的参数验证

显然，方法对其参数可能还有许多许多其他类型约束。例如，一个字符串参数可能不应为空字符串、不应仅由空格组成，或者必须以 "HTTPS" 作为前缀。列表 5.34 显示了完整的 `DownloadSSL()` 方法，演示了这种验证。

列表 5.34：DownloadSSL() 方法验证

```csharp
public class Program
{
    public static void main(string[] args)
    {
        int result = 0;
        if (args.Length != 2)
        {
            Console.WriteLine("Usage: Downloader <URL> <FileName>");
            result = 1;
        }
        else
        {
            DownloadSSL(args[0], args[1]);
            result = 0;
        }
    }

    private static void DownloadSSL(string httpsUrl, string fileName)
    {
        if (httpsUrl == null)
        {
            throw new ArgumentNullException(nameof(httpsUrl));
        }
        if (fileName == null)
        {
            throw new ArgumentNullException(nameof(fileName));
        }
        if (string.IsNullOrWhiteSpace(httpsUrl))
        {
            throw new ArgumentException("URL cannot be empty or whitespace");
        }
        if (string.IsNullOrWhiteSpace(fileName))
        {
            throw new ArgumentException("fileName cannot be empty or whitespace");
        }
        // ... implementation of DownloadSSL
    }
}
```

# 第 5 章：参数与方法

```csharp
#endif
if (!httpsUrl.ToUpper().StartsWith("HTTPS"))
{
    throw new ArgumentException("URL must start with HTTPS");
}

HttpClient client = new HttpClient();
byte[] response = client.GetByteArrayAsync(httpsUrl).Result;
File.WriteAllBytes(fileName, response);
Console.WriteLine($"Downloaded {response.Length} bytes to {fileName}");
```

使用 `TryParse()` 方法时，不再需要仅仅为了处理字符串到数字的转换而包含 `try/catch` 块。在预期场景中避免异常的另一个因素是性能。与大多数语言一样，C# 在抛出异常时会有轻微的性能损耗——花费的时间是微秒级，而大多数操作的时间是纳秒级。这种延迟在人类感官上通常是察觉不到的——除非异常未处理。例如，当执行列表 5.26 且用户输入无效年龄时，由于异常未被处理，运行时在搜索环境以查看是否有可加载的调试器时，会有明显的延迟。幸运的是，程序关闭时的性能缓慢通常不是一个需要担心的问题。

# 引入运算符

确定转换是否成功的唯一方法是尝试该操作并在其失败时捕获异常吗？抛出异常是一项相对昂贵的操作，最好在不进行异常处理的情况下尝试转换。为了这一目标，最好使用其中一种 `TryParse()` 方法，例如 `int.TryParse()`。它要求使用 `out` 关键字，因为 `TryParse()` 函数返回的是 `bool` 而不是转换后的值。列表 5.35 是一个演示使用 `int.TryParse()` 进行转换的代码片段。

列表 5.35：使用 int.TryParse() 进行转换

```csharp
if (int.TryParse(ageText, out int age))
{
    Console.WriteLine($"Hi {firstName}! You are {age * 12 } months old.");
}
else
{
    Console.WriteLine($"The age entered, {ageText}, is not valid.");
}
```

# 使用异常进行基础错误处理

考虑一下，我们在第 2 章中使用的 `int.Parse()` 方法，用于将字符串转换为整数。在这种情况下，预期用户输入始终是一个数字。`Parse()` 方法的一个问题是，当输入不是有效数字时它会抛出异常。

# 避免使用异常处理处理预期情况

开发者应该避免为预期情况抛出异常。例如，开发者不应预期用户会输入有效的文本。因此，与其依赖异常，开发者应该在尝试转换之前提供一种检查数据的手段。

> 指南
> 务必验证非空引用类型参数是否为空，如果是，则抛出 ArgumentNullException。
> 务必在 .NET 7.0 或更高版本中使用 ArgumentNullException.ThrowIfNull() 来验证值是否为空。

> 12. 通常情况下，开发者应该预期用户会执行意之外的操作；反之，他们应该编写防御性代码来处理“愚蠢的操作”。

