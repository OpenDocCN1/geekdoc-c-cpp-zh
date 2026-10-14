
```
}

var trades = new List<TradeRecord>();

var lineCount = 1;
foreach(var line in lines)
{
    var fields = line.Split(new char[] { ',' });

    if(fields.Length != 3)
    {
        Console.WriteLine("WARN: Line {0} malformed. Only {1} field(s) found.", lineCount, fields.Length);
        continue;
    }

    if(fields[0].Length != 6)
    {
        Console.WriteLine("WARN: Trade currencies on line {0} malformed: '{1}'", lineCount, fields[0]);
        continue;
    }

    int tradeAmount;
    if(!int.TryParse(fields[1], out tradeAmount))
    {
        Console.WriteLine("WARN: Trade amount on line {0} not a valid integer: '{1}'", lineCount, fields[1]);
    }

    decimal tradePrice;
    if(!decimal.TryParse(fields[2], out tradePrice))
    {
        Console.WriteLine("WARN: Trade price on line {0} not a valid decimal: '{1}'", lineCount, fields[2]);
    }

    var sourceCurrencyCode = fields[0].Substring(0, 3);
    var destinationCurrencyCode = fields[0].Substring(3, 3);

    // calculate values
    var trade = new TradeRecord
    {
        SourceCurrency = sourceCurrencyCode,
        DestinationCurrency = destinationCurrencyCode,
```

```
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
}
```

This is more than an example of a class that has too many responsibilities; it is also an example of a single method that has too many responsibilities. By reading the code carefully, you can discern

what this class is trying to achieve:

+   1. It reads every line from a Stream parameter, storing each line in a list of strings.
+   2. It parses out individual fields from each line and stores them in a more structured list of Trade-Record instances.
+   3. The parsing includes some validation and some logging to the console.
+   4. Each TradeRecord is enumerated, and a stored procedure is called to insert the trades into a database.

The responsibilities of the TradeProcessor are reading streams, parsing strings, validating fields, logging, and database insertion. The single responsibility principle states that this class, like all others, should only have a single reason to change. However, the reality of the TradeProcessor is that it will change under the following circumstances:

+   - When you decide not to use a Stream for input but instead read the trades from a remote call to a web service.
+   - When the format of the input data changes, perhaps with the addition of an extra field indicating the broker for the transaction.
+   - When the validation rules of the input data change.
+   - When the way in which you log warnings, errors, and information changes. If you are using a hosted web service, writing to the console would not be a viable option.
+   - When the database changes in some way—perhaps the insert_trade stored procedure requires a new parameter for the broker, too, or you decide not to store the data in a relational database and opt for document storage, or the database is moved behind a web service that you must call.

For each of these changes, this class would have to be modified. Furthermore, unless you maintain a variety of versions, there is no possibility of adapting the TradeProcessor so that it is able to read from a different input source, for example. Imagine the maintenance headache when you are asked to add the ability to store the trades in a web service, but only if a certain command-line argument was supplied.

## Refactoring for clarity

The first task on the road to refactoring the TradeProcessor so that it has one reason to change is to split the ProcessTrades method into smaller pieces so that each one focuses on a single responsibility. Each of the following listings shows a single method from the refactored TradeProcessor class, followed by an explanation of the changes.

First, Listing 5-2 shows the ProcessTrades method, which now does nothing more than delegate to other methods.

# LISTING 5-2

The ProcessTrades method is very minimal because it delegates work to other methods.

[Click here to view code image](#)

```
public void ProcessTrades(System.IO.Stream stream)
{
```

```
var lines = ReadTradeData(stream);
var trades = ParseTrades(lines);
StoreTrades(trades);
}
```

The original code was characterized by three distinct parts of a process—reading the trade data from a stream, converting the string data in the stream to TradeRecord instances, and writing the trades to persistent storage. Note that the output from one method feeds into the input to the next method. You cannot call StoreTrades until you have the trade records returned from the Parse-Trades method, and you cannot call ParseTrades until you have the lines returned from the ReadTradeData method.

Taking each of these methods in order, let’s look at ReadTradeData, in Listing 5-3.

# LISTING 5-3 ReadTradeData encapsulates the original code.

Click here to view code image

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

This code is preserved from the original implementation of the ProcessTrades method. It has simply been encapsulated in a method that returns the resultant string data as a string enumeration. Note that this makes the return value read-only, whereas the original implementation unnecessarily allowed subsequent parts of the process to add further lines.

The ParseTrades method, shown in Listing 5-4, is next. It has changed somewhat from the original implementation because it, too, delegates some tasks to other methods.

# LISTING 5-4 ParseTrades delegates to other methods to limit its complexity.

Click here to view code image

```
private IEnumerable<TradeRecord> ParseTrades(IEnumerable<string> tradeData)
{
```

```
```csharp
var trades = new List<TradeRecord>();
var lineCount = 1;
foreach (var line in tradeData)
{
    var fields = line.Split(new char[] { ',' });

    if(!ValidateTradeData(fields, lineCount))
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
```

This method delegates validation and mapping responsibilities to other methods. Without this delegation, this section of the process would still be too complex and it would retain too many responsibilities. The ValidateTradeData method, shown in [Listing 5-5](#), returns a Boolean value to indicate whether any of the fields for a trade line are invalid.

# **LISTING 5-5** All of the validation code is in a single method.

[Click here to view code image](#)

```
```csharp
private bool ValidateTradeData(string[] fields, int currentLine)
{
    if(fields.Length != 3)
    {
        LogMessage("WARN: Line {0} malformed. Only {1} field(s) found.", currentLine,
            fields.Length);
        return false;
    }

    if(fields[0].Length != 6)
    {
        LogMessage("WARN: Trade currencies on line {0} malformed: '{1}'", currentLine,
            fields[0]);
        return false;
```
```
