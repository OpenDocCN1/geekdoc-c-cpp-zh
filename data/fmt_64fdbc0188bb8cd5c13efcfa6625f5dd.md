
# C# 入门教程

## URL 模板常量

```csharp
private const string urlTemplateYahoo = "http://chart.finance.yahoo.com/table.csv?s={0}&d={1}&e={2}&f={3}&g&a={1}&b={2}&c={4}&ignore=.csv";

private const string urlTemplateNasdaq = "http://nasdaq.com/ext/charts/d2-1-14-0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0";
```

## 需求概述

你还需要添加一个名为 `IsInternetAvailable` 的 `bool` 属性，它将返回调用 `System.Net.NetworkInformation` 命名空间下 `NetworkInterface` 类的 `GetIsNetworkAvailable` 方法的结果。此属性将用于确保计算机上有可用的互联网连接。

由于你将使用异步请求，你需要在 `TaskScheduler` 类中实现 `UnobservedTaskException` 事件以处理被取消的 Task。因为只有第一个返回结果的结果会被使用，其余的将被取消，.NET Framework 要求对被取消的 Task 进行观察，以避免垃圾回收为这些 Task 抛出异常。可以通过在 `UnobservedTaskException` 事件中调用 `e.SetObserved` 方法来忽略 `CancelledObserved`。

- 在 `Classes` 文件夹中添加名为 `Factory` 的类。
- 添加一个名为 `urlTemplateYahoo` 的私有字符串常量（请见上方描述的使用的 URL 模板）。
- 添加一个名为 `urlTemplateNasdaq` 的私有字符串常量（请见上方描述的使用的 URL 模板）。
- 添加一个名为 `InternetAvailable` 的 `bool` 属性，如果计算机上有可用互联网连接则返回 `true`。

```csharp
public static bool IsInternetAvailable
{
    get { return NetworkInterface.GetIsNetworkAvailable(); }
}
```

- 添加一个公共构造函数并使用 `UnobservedTaskException` 事件。`TaskScheduler.UnobservedTaskException += new EventHandler<UnobservedTaskExceptionEventArgs>(UnobservedTaskException_Handler);`
- 将事件方法设为静态，以便供所有实例使用。
- 在事件中调用 `e.SetObserved` 方法，告诉垃圾回收你已经观察了被取消的对象，可以将其移除。

## StockFactory 类实现

到目前为止 `StockFactory` 类的代码：

```csharp
class StockFactory
{
    #region Constants

    private const string urlTemplateYahoo = "http://chart.finance.yahoo.com/table.csv?s={0}&d={1}&e={2}&f={3}&g&a={1}&b={2}&c={4}&ignore=.csv";

    private const string urlTemplateNasdaq = "http://charting.nasdaq.com/ext/charts.dll?d2-1-14-0-0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0";

    #endregion

    #region Properties

    public static bool IsInternetAvailable
    {
        get { return NetworkInterface.GetIsNetworkAvailable(); }
    }

    #endregion

    #region Constructor

    public static StockFactory()
    {
        /* 当异步请求被取消时，会抛出异常。
           必须观察这些异常，以避免垃圾回收在清理
           Task 对象期间抛出异常。 */
        TaskScheduler.UnobservedTaskException += new EventHandler<UnobservedTaskExceptionEventArgs>(TaskUnobservedException_Handler);
    }

    #endregion

    #region Event Handlers

    /* 在此应用程序中，启动了多个 Task 来获取股票
       数据，但只有第一个返回的 Task 会被处理，其他
       Task 将被取消。已取消的 Task 需要被观察，
       否则垃圾回收将在清理 Task 对象期间抛出异常。
       以下事件处理程序是解决此问题的变通方法。
       注意：此构造函数仅应与类注册一次。 */
    private static void TaskUnobservedException_Handler(object sender, UnobservedTaskExceptionEventArgs e)
    {
        /* 忽略所有后续的任务，因为第一个返回结果的
           Task 结果已经处理过了 */
        e.SetObserved();
    }

    #endregion
}
```

## ParsePrices 方法

`ParsePrices` 方法将从 `GetStockAsync` 方法调用，并使用传入的 `WebResponse` 对象读取其响应流，并分离出从网站返回的历史价格信息。

添加一个 `try/finally` 块，其中 `finally` 块关闭通过 `response` 参数传递给方法的响应流。

使用响应对象上的 `GetResponseStream` 方法来获取 `try` 块中包含数据的响应流。

使用 `StreamReader` 读取数据；继续读取流，直到 `EndOfStream` 属性为 `true`。

从流读取器中逐行读取数据，并使用 `Split` 方法和 `separators` 参数进行分割。将结果存储在名为 `tokens` 的 `string[]` 变量中。

检查 `tokens` 中的第一个标记是有效值，以及存储在传入的 `dataIndex` 参数确定的位置的价格是否解析为 `decimal` 值。使用 `en-US` 文化以确保数据被正确解析。将价格添加到名为 `prices` 的 `List<decimal>` 集合。

在读取响应流的 `using` 块下方返回 `prices` 集合。

### 实现步骤

1. 为 `StockFactory` 类添加一个私有静态 `List<decimal>` 方法 `ParsePrices`。该方法有三个参数：类型为 `WebResponse` 的 `response`、类型为 `char[]` 的 `separators` 和类型为 `int` 的 `dataIndex`。
2. 为方法添加一个 `try/finally` 块，其中 `finally` 块关闭响应流。
3. 在 `try` 块中添加名为 `prices` 的 `List<decimal>` 集合。
4. 为响应对象上的 `GetResponseStream` 方法调用添加 `using` 块，使用 `(Stream webStream = response.GetResponseStream())`。
5. 为 `StreamReader` 添加 `using` 块，以读取响应流的内容，使用 `(StreamReader reader = new StreamReader(webStream))`。
6. 添加一个 `while` 循环，只要流中还有内容就一直迭代。

```csharp
while (!reader.EndOfStream)
```

7. 在循环内部逐行读取，并将数据存储在名为 `record` 的字符串变量中。
8. 使用 `separators` 参数和 `Split` 方法分割 `record`。将结果存储在名为 `tokens` 的 `string[]` 变量中。
9. 添加一个名为 `date` 的 `DateTime` 变量和一个名为 `data` 的 `decimal` 变量，用于存储从 `TryParse` 方法从 `tokens` 返回的值。
10. 将 `tokens` 数组中的第一个值解析为日期，并将价格添加到 `dataIndex` 变量值对应的集合中。如果解析成功则添加。

```csharp
if (DateTime.TryParse(tokens[0], out date))
{
    if (Decimal.TryParse(tokens[dataIndex],
        NumberStyles.AllowDecimalPoint,
        new CultureInfo("en-US"), out data))
    {
        prices.Add(data);
    }
}
```

11. 在其他 `using` 块下方从方法返回 `prices` 集合。

### 完整代码

```csharp
/// <summary>
/// 从响应流解析价格
/// </summary>
private static List<decimal> ParsePrices(WebResponse response, char[] separators, int dataIndex)
{
    // 打开数据流并解析
    try
    {
        List<decimal> prices = new List<decimal>();

        using (Stream webStream = response.GetResponseStream())
        {
            using (StreamReader reader = new StreamReader(webStream))
            {
                // 读取流
                while (!reader.EndOfStream)
                {
                    // 逐行读取
                    string record = reader.ReadLine();

                    // 分割记录
                    string[] tokens = record.Split(separators);

                    DateTime date;
                    decimal data;

                    // 使用 en-US 文化确保数据解析正确
                    if (DateTime.TryParse(tokens[0], out date))
                    {
                        if (Decimal.TryParse(tokens[dataIndex],
                            NumberStyles.AllowDecimalPoint,
                            new CultureInfo("en-US"), out data))
                        {
                            prices.Add(data);
                        }
                    }
                }
            }
        }

        // 返回集合
        return prices;
    }
    finally
    {
        // 在返回之前关闭响应流
        response.Close();
    }
}
```

## GetStockAsync 方法

此静态方法将从 `GetStockData` 方法调用，通过对方法参数中指定的网站进行异步调用来获取股票信息。该方法具有以下参数：`url` 类型为 `string`、`site` 类型为 `string`、`dataSource` 类型为 `string`、`symbol` 类型为 `string`、`separators` 类型为 `char[]`、`index` 类型为 `int`、`yearsOfHistory` 类型为 `int` 以及声明为 `out` 的 `request` 类型。

要执行异步请求，你必须使用 `url` 参数创建请求并将其存储在定义的 `out` 关键字参数中。你通过调用 `HttpRequest` 类的 `Create` 方法创建请求。

要进行异步调用，你必须使用 `Task.Factory.FromAsync` 方法创建一个名为 `webTask` 的 Task，传入你创建的请求对象的 `BeginGetResponse` 和 `EndGetResponse` 方法。

由于你想在另一个名为 `resultTask` 的 Task 中使用 `webTask` 的结果，你需要使用 `ContinueWith` 在任务结束的地方继续。传递 Lambda 表达式的 `antecedent` 参数包含第一个 Task 的响应。如果 `Status` 属性不等于 `TaskStatus.Faulted`，则调用 `ParsePrices` 方法读取响应流并读取价格信息；将结果存储在名为 `prices` 的 `List<decimal>` 集合中。返回一个新的 `Stock` 实例并传递 `symbol`、`site` 和 `dataSource` 参数的值。

如果 `antecedent` 参数等于 `TaskStatus.Faulted`，则返回一个新的 `Stock` 实例，并传递 `symbol`、`site` 和 `dataSource` 参数的值以及空的 `List<decimal>` 集合。

方法返回 `resultTask` 变量的值。

### 实现步骤

- 为 `StockFactory` 类添加一个具有上述参数的 `Task<Stock>` 方法 `GetStockAsync`。

```csharp
private static Task<Stock> GetStockAsync(string url, string site, string dataSource, string symbol, char[] separators, int dataIndex, int yearsOfHistory, out HttpWebRequest request)
```

- 使用 `url` 参数创建 `HttpWebRequest` 实例并将其存储在传入方法的 `out` 关键字参数中。

```csharp
request = (HttpWebRequest)HttpWebRequest.Create(url);
```

- 添加名为 `webTask` 的 Task 以执行异步 Web 请求。

```csharp
var webTask = Task.Factory.FromAsync<WebResponse>(
    request.BeginGetResponse,
    request.EndGetResponse,
    null);
```

- 添加名为 `resultTask` 的回调 Task，它将使用异步调用的结果。

```csharp
var resultTask = webTask.ContinueWith<Stock>(antecedent =>
{
    if (!antecedent.Status.Equals(TaskStatus.Faulted))
    {
        // 成功处理逻辑
    }
    else
    {
        // 故障处理逻辑
    }
});
```

- 在回调 Task 中添加一个 `if` 语句，检查 `webTask` Task 是否以故障状态返回。

```csharp
if (!antecedent.Status.Equals(TaskStatus.Faulted))
```
