Because you moved all of the code from ProcessTrades into separate methods in the first refactor, you should have a good idea of where the first abstractions should be applied. As prescribed by the single responsibility principle, the three main responsibilities will be handled by different classes. As you know from previous chapters, you should not have direct dependencies from one class to another but should instead work via interfaces. Therefore, the three responsibilities are factored out into three separate interfaces. Listing 7-9 shows how the TradeProcessor class looks after this change.

# LISTING 7-9

The TradeProcessor is now the encapsulation of a process, and nothing more.

```
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

The class is now significantly different from its previous incarnation. It no longer contains the implementation details for the whole process but instead contains the *blueprint* for the process. The class models the process of transferring trade data from one format to another. This is its only responsibility, its only concern, and the only reason that this class should change. If the process itself changes, this class will change to reflect it. But if you decide you no longer want to retrieve data from a Stream, log to the console, or store the trades in a database, this class remains as is.

The interfaces that the TradeProcessor now depends on all live in a separate assembly. This ensures that neither the client nor the implementation assemblies reference each other. Also separated into another assembly are the three classes that implement these interfaces, the StreamTradeDataProvider, SimpleTradeParser, and AdoNetTradeStorage classes. Note that there is a naming convention used for these classes. First, the prefixed I was removed from the interface name and replaced with the implementation-specific context that is required of the class. So StreamTradeDataProvider allows you to infer that it is an implementation of the ITradeDataProvider interface that retrieves its data from a Stream object. The AdoNetTradeStorage class uses ADO.NET to persist the trade data. I have prefixed the ITradeParser implementation with the word Simple to indicate that it has no dependency context.