

```csharp
var sourceCurrencyCode = fields[0].Substring(0, 3);
var destinationCurrencyCode = fields[0].Substring(3, 3);

// calculate values
var trade = new TradeRecord
{
    SourceCurrency = sourceCurrencyCode,
    DestinationCurrency = destinationCurrencyCode,
    Lots = tradeAmount / LotSize,
    Price = tradePrice
};

trades.Add(trade);

lineCount++;
}

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

Console.WriteLine("INFO: {0} trades processed", trades.Count);

private static float LotSize = 100000f;
}
```

这不仅仅是一个职责过多的类的例子；它也是一个单一方法职责过多的例子。仔细阅读代码，你可以看出这个类试图实现什么：

1. 它从 `Stream` 参数中读取每一行，将每一行存储在一个字符串列表中。
2. 它从每一行中解析出各个字段，并将它们存储在一个更结构化的 `TradeRecord` 实例列表中。
3. 解析过程包括一些验证和向控制台的日志记录。
4. 遍历每个 `TradeRecord`，并调用存储过程将交易插入数据库。

`TradeProcessor` 的职责包括读取流、解析字符串、验证字段、记录日志以及数据库插入。单一职责原则指出，这个类与其他类一样，应该只有一个变更原因。然而，`TradeProcessor` 的实际情况是，它会在以下情况下发生变化：

- 当你决定不再使用 `Stream` 作为输入，而是改为从 Web 服务的远程调用读取交易时。
- 当输入数据的格式发生变化时，例如增加一个表示该笔交易经纪商的额外字段。
- 当输入数据的验证规则发生变化时。
- 当你记录警告、错误和信息的方式发生变化时。如果使用的是托管 Web 服务，写入控制台就不再是一个可行的选项。
- 当数据库以某种方式发生变化时——例如 `insert_trade` 存储过程也需要经纪商的新参数，或者你决定不再将数据存储在关系数据库中而选择文档存储，或者数据库被移至你必须调用的 Web 服务之后。

对于每一次这样的变更，这个类都必须被修改。此外，除非你维护多种版本，否则没有可能使 `TradeProcessor` 能够从不同的输入源读取，例如。想象一下，当被要求添加将交易存储到 Web 服务的能力，但仅在提供特定命令行参数时才生效时，会带来多大的维护难题。

## 为清晰而重构

重构 `TradeProcessor` 使其只有一个变更原因的道路上的第一项任务，是将 `ProcessTrades` 方法拆分为更小的方法，使每个方法都专注于单一职责。以下每个清单都展示了重构后的 `TradeProcessor` 类中的一个方法，然后是对更改的解释。

首先，清单 7-2 显示了 `ProcessTrades` 方法，它现在除了委托给其他方法之外什么都不做。

**LISTING 7-2** `ProcessTrades` 方法非常简洁，因为它将工作委托给其他方法。

```csharp
public void ProcessTrades(System.IO.Stream stream)
{
    var lines = ReadTradeData(stream);
    var trades = ParseTrades(lines);
    StoreTrades(trades);
}
```

原始代码的特点是该过程有三个不同的部分——从流中读取交易数据、将流中的字符串数据转换为 `TradeRecord` 实例，以及将交易写入持久存储。请注意，一个方法的输出会作为输入传递给下一个方法。你不能在 `ParseTrades` 方法返回交易记录之前调用 `StoreTrades`，也不能在 `ReadTradeData` 方法返回行之前调用 `ParseTrades`。

按顺序来看这些方法，让我们先看 `ReadTradeData`，见清单 7-3。

**LISTING 7-3** `ReadTradeData` 封装了原始代码。

```csharp
private IEnumerable<string> ReadTradeData(System.IO.Stream stream)
{
    var tradeData = new List<string>();
    using (var reader = new System.IO.StreamReader(stream))
    {
        string line;
        while ((line = reader.ReadLine()) != null)
        {
            tradeData.Add(line);
        }
    }
    return tradeData;
}
```

这段代码保留自 `ProcessTrades` 方法的原始实现。它只是被封装在一个返回结果字符串数据作为字符串枚举的方法中。请注意，这使得返回值变为只读，而原始实现不必要地允许流程的后续部分添加更多行。

接下来是 `ParseTrades` 方法，见清单 7-4。它与原始实现相比有所变化，因为它也将一些任务委托给其他方法。

**LISTING 7-4** `ParseTrades` 委托给其他方法以限制其复杂性。

```csharp
private IEnumerable<TradeRecord> ParseTrades(IEnumerable<string> tradeData)
{
    var trades = new List<TradeRecord>();
    var lineCount = 1;
    foreach (var line in tradeData)
    {
        var fields = line.Split(new char[] { ',' });

        if (!ValidateTradeData(fields, lineCount))
        {
            continue;
        }

        var trade = MapTradeDataToTradeRecord(fields);

        trades.Add(trade);

        lineCount++;
    }
    return trades;
}
```

该方法将验证和映射职责委托给其他方法。如果没有这种委托，该流程的这一部分仍然过于复杂，并且会保留过多的职责。`ValidateTradeData` 方法，见清单 7-5，用于返回布尔值以指示交易行的任何字段是否无效。

**LISTING 7-5** 所有验证代码都在一个方法中。

```csharp
private bool ValidateTradeData(string[] fields, int currentLine)
{
    if (fields.Length != 3)
    {
        LogMessage("WARN: Line {0} malformed. Only {1} field(s) found.", currentLine, fields.Length);
        return false;
    }

    if (fields[0].Length != 6)
    {
        LogMessage("WARN: Trade currencies on line {0} malformed: '{1}'", currentLine, fields[0]);
        return false;
    }

    int tradeAmount;
    if (!int.TryParse(fields[1], out tradeAmount))
    {
        LogMessage("WARN: Trade amount on line {0} not a valid integer: '{1}'", currentLine, fields[1]);
        return false;
    }

    decimal tradePrice;
    if (!decimal.TryParse(fields[2], out tradePrice))
    {
        LogMessage("WARN: Trade price on line {0} not a valid decimal: '{1}'", currentLine, fields[2]);
        return false;
    }

    return true;
}
```

对原始验证代码所做的唯一更改是它现在委托给另一个方法进行日志记录。不是在需要时嵌入对 `Console.WriteLine` 的调用，而是使用 `LogMessage` 方法，见清单 7-6。

**LISTING 7-6** `LogMessage` 方法目前只是 `Console.WriteLine` 的同义词。

```csharp
private void LogMessage(string message, params object[] args)
{
    Console.WriteLine(message, args);
}
```

回到 `ParseTrades` 方法的调用栈，清单 7-7 显示了它委托的另一个方法。该方法将表示流中各个字段的字符串数组映射到 `TradeRecord` 类的实例。

**LISTING 7-7** 从一种类型到另一种类型的映射是单独的职责。

```csharp
private TradeRecord MapTradeDataToTradeRecord(string[] fields)
{
    var sourceCurrencyCode = fields[0].Substring(0, 3);
    var destinationCurrencyCode = fields[0].Substring(3, 3);
    var tradeAmount = int.Parse(fields[1]);
    var tradePrice = decimal.Parse(fields[2]);
```

