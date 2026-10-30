

```csharp
var tradeRecord = new TradeRecord
{
    SourceCurrency = sourceCurrencyCode,
    DestinationCurrency = destinationCurrencyCode,
    Lots = tradeAmount / LotSize,
    Price = tradePrice
};

return tradeRecord;
}
```

本次重构引入的第六个也是最后一个新方法是 StoreTrades，见清单 7-8。该方法封装了与数据库交互的代码。它还将信息日志消息委托给前述的 LogMessage 方法。

## LISTING 7-8

现在 StoreTrades 方法已就位，该类中的职责已得到清晰划分。

```csharp
private void StoreTrades(IEnumerable<TradeRecord> trades)
{
    using (var connection = new System.Data.SqlClient.SqlConnection("Data Source=(local);Initial Catalog=TradeDatabase;Integrated Security=True"))
    {
        connection.Open();
        using (var transaction = connection.BeginTransaction())
        {
            foreach (var trade in trades)
            {
                var command = connection.CreateCommand();
                command.Transaction = transaction;
                command.CommandType = System.Data.CommandType.StoredProcedure;
                command.CommandText = "dbo.insert_trade";
                command.Parameters.AddWithValue("@sourceCurrency", trade.SourceCurrency);
                command.Parameters.AddWithValue("@destinationCurrency", trade.DestinationCurrency);
                command.Parameters.AddWithValue("@lots", trade.Lots);
                command.Parameters.AddWithValue("@price", trade.Price);

                command.ExecuteNonQuery();
            }

            transaction.Commit();
        }
        connection.Close();
    }
    LogMessage("INFO: {0} trades processed", trades.Count());
}
```

回顾这次重构，可以看出它是对原始实现的明显改进。然而，你到底实现了什么？尽管新的 ProcessTrades 方法无可争议地比单体原始方法更小，代码也更具可读性，但你在适应性方面几乎没有获得什么。你可以更改 LogMessage 方法的实现，使其例如写入文件而不是写入控制台，但这需要对 TradeProcessor 类进行更改，而这正是你想要避免的。

这次重构是通向真正分离该类职责道路上的重要一步。它是为了清晰而进行的重构，而不是为了适应性。下一步任务是将每个职责拆分到不同的类中并置于接口之后。你需要真正的抽象来实现有用的适应性。

## Refactoring for abstraction

在新的 TradeProcessor 实现的基础上，下一次重构引入了若干抽象，从而使你能够处理该类的几乎任何变更请求。虽然这个运行示例可能看起来非常小，甚至微不足道，但对于本教程的目的来说，它是一个可行的构造。此外，像这样的小型应用程序发展成更大规模的东西是很常见的。当几个人开始使用它时，功能请求就会开始增加。

通常，术语原型和概念验证会被应用于此类所谓的微小应用程序，而从原型到生产应用程序的转换相对无缝。这就是为什么能够向抽象重构是适应性开发的试金石的原因。没有它，无数的请求会退化为“大泥球”——一个类，或程序集中的一组类，职责划分不清且没有可辨别的抽象。结果是一个没有单元测试、难以维护和增强的应用程序，而它本可能是业务线中的关键部分。

对 TradeProcessor 进行抽象重构的第一步是设计它将用于执行读取、处理和存储交易数据的三个高级任务的接口或接口。图 7-1 显示了第一组抽象。

![](img/f852e0a12c174e64d91a8e1a05146eab_249_0.png)

**FIGURE 7-1** The TradeProcessor will now depend on three new interfaces.

由于你在第一次重构中将 ProcessTrades 中的所有代码移入了单独的方法，你应该对第一个抽象应应用的位置有很好的了解。正如单一职责原则所规定，三个主要职责将由不同的类处理。正如你从前几章所知，不应在一个类到另一个类之间有直接依赖，而应通过接口工作。因此，这三个职责被分解为三个独立的接口。清单 7-9 显示了此更改后 TradeProcessor 类的样子。

## LISTING 7-9

The TradeProcessor is now the encapsulation of a process, and nothing more.

```csharp
public class TradeProcessor
{
    public TradeProcessor(ITradeDataProvider tradeDataProvider, ITradeParser tradeParser,
    ITradeStorage tradeStorage)
    {
        this.tradeDataProvider = tradeDataProvider;
        this.tradeParser = tradeParser;
        this.tradeStorage = tradeStorage;
    }

    public void ProcessTrades()
    {
        var lines = tradeDataProvider.GetTradeData();
        var trades = tradeParser.Parse(lines);
        tradeStorage.Persist(trades);
    }

    private readonly ITradeDataProvider tradeDataProvider;
    private readonly ITradeParser tradeParser;
    private readonly ITradeStorage tradeStorage;
}
```

该类现在与之前的版本有显著不同。它不再包含整个过程的实现细节，而是包含该过程的 *blueprint*。该类对交易数据从一种格式转移到另一种格式的过程建模。这是它的唯一职责、唯一关注点，也是该类应该更改的唯一原因。如果过程本身发生变化，该类将随之改变以反映它。但如果你决定不再想从 Stream 检索数据、向控制台记录日志或将交易存储在数据库中，该类保持不变。

TradeProcessor 现在依赖的接口都位于单独的程序集中。这确保了客户端和实现程序集彼此不引用。另有三个实现这些接口的类也分离到另一个程序集中，即 StreamTradeDataProvider、SimpleTradeParser 和 AdoNetTradeStorage 类。请注意，这些类使用了命名约定。首先，从接口名称中删除了前缀 I 并替换为类所需的具体上下文。因此，StreamTradeDataProvider 让你可以推断它是从 Stream 对象检索数据的 ITradeDataProvider 接口的实现。AdoNetTradeStorage 类使用 ADO.NET 来持久化交易数据。我在 ITradeParser 实现前加上了 Simple 这个词，以表明它没有依赖上下文。

可以从此示例中提取更多抽象。请记住，原始的 ParseTrades 方法将验证和映射的职责委托出去了。你可以重复重构过程，以便 SimpleTradeParser 类不承担超过一个职责。图 7-2 以统一建模语言 UML 显示了如何实现这一点。

![](img/f852e0a12c174e64d91a8e1a05146eab_252_0.png)

**FIGURE 7-2** The SimpleTradeParser is also refactored to ensure that each class has a single responsibility.

将职责抽象为接口及其配套实现的过程是递归的。当你检查每个类时，必须确定它所承担的职责并将其分解，直到该类只有一个职责为止。清单 7-11 显示了 SimpleTradeParser 类，它在适当的地方委托给接口。它的唯一变更原因是如果交易数据的整体结构发生变化——例如，如果数据不再使用逗号分隔值而改为使用制表符，或许是 XML。

## LISTING 7-11

The algorithm for parsing trade data is encapsulated in ITradeParser implementations.

```csharp
public class SimpleTradeParser : ITradeParser
{
    public SimpleTradeParser(ITradeValidator tradeValidator, ITradeMapper tradeMapper)
    {
        this.tradeValidator = tradeValidator;
        this.tradeMapper = tradeMapper;
    }

    public IEnumerable<TradeRecord> Parse(IEnumerable<string> tradeData)
    {
        var trades = new List<TradeRecord>();
        var lineCount = 1;
        foreach (var line in tradeData)
        {
            var fields = line.Split(new char[] { ',' });
```
