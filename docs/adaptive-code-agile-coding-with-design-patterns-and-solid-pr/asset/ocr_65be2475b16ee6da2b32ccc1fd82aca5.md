# Refactoring for clarity

The first task on the road to refactoring the TradeProcessor so that it has one reason to change is to split the ProcessTrades method into smaller methods so that each one focuses on a single responsibility. Each of the following listings shows a single method from the refactored TradeProcessor class, followed by an explanation of the changes.

First, Listing 7-2 shows the ProcessTrades method, which now does nothing more than delegate to other methods.

LISTING 7-2 The ProcessTrades method is very minimal because it delegates work to other methods.

```
public void ProcessTrades(System.IO.Stream stream)
{
    var lines = ReadTradeData(stream);
    var trades = ParseTrades(lines);
    StoreTrades(trades);
}
```

The original code was characterized by three distinct parts of a process—reading the trade data from a stream, converting the string data in the stream to TradeRecord instances, and writing the trades to persistent storage. Note that the output from one method feeds into the input to the next method. You cannot call StoreTrades until you have the trade records returned from the ParseTrades method, and you cannot call ParseTrades until you have the lines returned from the ReadTradeData method.

Taking each of these methods in order, let's look at ReadTradeData, in Listing 7-3.

LISTING 7-3 ReadTradeData encapsulates the original code.

```
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