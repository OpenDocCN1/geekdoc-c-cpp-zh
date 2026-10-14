```
}

int tradeAmount;
if (!int.TryParse(fields[1], out tradeAmount))
{
    LogMessage("WARN: Trade amount on line {0} not a valid integer: '{1}'",
    currentLine, fields[1]);
    return false;
}

decimal tradePrice;
if (!decimal.TryParse(fields[2], out tradePrice))
{
    LogMessage("WARN: Trade price on line {0} not a valid decimal: '{1}'",
    currentLine, fields[2]);
    return false;
}

return true;
}
```

The only change made to the original validation code is that it now delegates to yet another method for logging messages. Rather than embedding calls to Console.WriteLine where needed, the LogMessage method is used, shown in Listing 5-6.

# LISTING 5-6 The LogMessage method is currently just a synonym for Console.WriteLine.

Click here to view code image

```
private void LogMessage(string message, params object[] args)
{
    Console.WriteLine(message, args);
}
```

Returning up the stack to the ParseTrades method, Listing 5-7 shows the other method to which it delegates. This method maps an array of strings representing the individual fields from the stream to an instance of the TradeRecord class.

# LISTING 5-7 Mapping from one type to another is a separate responsibility.

Click here to view code image