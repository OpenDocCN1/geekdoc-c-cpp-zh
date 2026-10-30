
{
    Console.WriteLine("WARN: Trade price on line {0} not a valid decimal: '{1}'", lineCount, fields[2]);
}

var sourceCurrencyCode = fields[0].Substring(0, 3);
var destinationCurrencyCode = fields[0].Substring(3, 3);

// 计算值
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
        foreach(var trade in trades)
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
}

private static float LotSize = 100000f;

这段代码更偏向过程式，而不是面向对象。它是一份很长的操作步骤，用于将一种格式的数据——流——转换为另一种格式的数据——关系数据库。它可能最初只是一个原型、一次技术验证，或者仅仅是一个非常快速且粗糙的解决方案。但和常见情况一样，现在需要将其重新调整为更健壮、功能更完善的解决方案。如果你遇到这样的代码，可能会想直接修改它，直到它处于更好的状态：更加面向对象、提供扩展点，并且更易于测试。这确实是个好主意，但执行过程会充满风险：没有测试这个安全网来指出错误，重构就容易出现最隐蔽的一类故障：静默失败。在没有测试的情况下重构代码，前提步骤是尽可能记录其当前行为。

## 特征测试

第一个目标是收集代码在各种输入下产生的结果。通过定义并提供一系列输入，你可以确定输出的范围。这可以是一个手动过程：多次运行应用程序，并记录每个输入对应的输出。但显然，这种方式难以扩展，而且执行起来会耗费很长时间。因此，更好的做法是将这一过程自动化，形成特征测试。

尽管名称如此，但你不会将特征测试实现为单元测试。这是因为你不会一直运行特征测试。特征测试的输出，是在给定特定输入时当前行为的集合。之后，当你创建黄金主测试时，这些输出将成为你的预期结果。预期结果不会经常改变，只有在准备为代码添加功能或改变其当前行为时才会改变。如果将特征测试实现为单元测试，那么你要么会在每次运行全部测试时错误地重新生成预期结果，要么会在大部分开发过程中注释掉特征测试，只在某个预期结果失败时取消注释。这很容易出错。因此，特征测试将被实现为一个持续运行的控制台应用程序。代码清单 6-18 展示了第一个特征测试。

```
class Program
{
    static void Main(string[] args)
    {
        var inputs = new List<string>()
        {
            "empty-file.txt"
        };

        var originalConsoleOut = Console.Out;

        foreach (var input in inputs)
        {
            var tradeStream = Assembly.GetExecutingAssembly()
                .GetManifestResourceStream(typeof(Program), input);

            using (var streamWriter = new StreamWriter(
                File.OpenWrite($"expectation-{input}")))
```

```
```csharp
{
    Console.SetOut(streamWriter);

    var tradeProcessor = new TradeProcessorService();
    tradeProcessor.ProcessTrades(tradeStream);
}
}

Console.SetOut(originalConsoleOut);

Console.ReadKey();
}
```
```

这段代码会捕获 `ProcessTrades` 方法写入控制台的所有内容，并将其重定向到输出文件。尽管可能会生成许多输入和输出对，但目前只提供了一个：空文件。很快还会添加几个示例，这些输出文件稍后将为黄金主测试提供预期结果。正如你所看到的，这是一种粗粒度的方式，用于为未经测试、并且很可能难以测试的代码搭建一些测试。如果能够模拟 `TradeProcessor` 类中嵌入的数据库交互当然很好，但在不可能破坏功能的情况下，这并不可行。对于复杂程度甚至高于这个示例的代码，如果不先建立安全网，直接进行重构，风险通常会更高。

运行这个特征测试后，会生成一个包含以下内容的输出文件。

```
```text
INFO: 0 trades processed
```
```

表 6-1 展示了特征测试的其他一些输入和输出对。

**表 6-1** 特征测试输入和预期输出。

| 名称 | 输入 | 输出 |
|---|---|---|
| 空文件 |  | INFO: 0 trades processed |
| 一个字段 | Test | WARN: Line 1 malformed. Only 1 field(s) found.\nINFO: 0 trades processed |
| 格式错误的货币对 | Test,123,abc | WARN: Trade currencies on line 1 malformed: 'Test'\nINFO: 0 trades processed |
| 交易量无效 | GBPUSD,xyz,abc | WARN: Trade amount on line 1 not a valid integer: 'xyz'\nWARN: Trade price on line 1 not a valid decimal: 'abc'\nINFO: 1 trades processed |
| 交易金额无效 | GBPUSD,100,abc | WARN: Trade price on line 1 not a valid decimal: 'abc'\nINFO: 1 trades processed |
| 格式正确 | GBPUSD,1000,0.81 | INFO: 1 trades processed |

这组输入和输出并不完整，也不可能完整。你捕获的测试越多，重构时就越有信心，因此单个输入和输出对不太可能足够。但在捕获大量特殊输入时，收益会逐渐降低。

## 为遗留代码添加检测

遗留代码通常不像本例这样有帮助；甚至可能根本没有可供捕获的控制台输出。实际上，即使是支持特征测试所需的最基本基础设施，也可能需要在现有代码中进行一些修改，而此时还没有测试作为保障。这是很常见的现实，因为大多数遗留代码从未被设计为可测试。因此，你可能需要在待重构的类或方法中的某些位置添加控制台日志。通常，这类日志会添加在分支和循环表达式周围，也会添加在产生副作用的代码部分附近，例如向数据库写入数据或引发事件的地方。

说这些改动并非真正意义上的变更，并不完全是在故意误导。它们不是修订，而是追加。追加改动仍然存在破坏功能的风险；只是与修改已有代码行相比，追加改动对现有代码造成不利影响的可能性更低。

## 黄金主测试

完成一组特征测试后，你现在可以着手创建黄金主测试。该测试会获取特征测试的输出，并将其作为断言时使用的预期结果。这些测试将作为单元测试实现，并且可以像往常一样运行。不过请记住，严格来说，这些并不是单元测试，因为它们依赖文件系统等外部因素。因此，它们既不够隔离，也不够快速，不能被视为单元测试。代码清单 6-19 展示了黄金主测试。

代码清单 6-19 黄金主测试。

```
public class GoldenMaster
{
    private static string CharacterizationTestOutput =
        Path.Combine("../../../..", "CharacterizationTests/bin/Debug/");

    [Fact]
    public void OutputStillMatchesCharacterization()
    {
        var inputsAndExpectations = new Dictionary<string, string>()
        {
            { "empty-file.txt", "expectation-empty-file.txt" },
            { "one-field.txt", "expectation-one-field.txt" },
            { "malformed-currency-pair.txt", "expectation-malformed-currency-pair.txt" },
            { "trade-volume-invalid.txt", "expectation-trade-volume-invalid.txt" },
```
