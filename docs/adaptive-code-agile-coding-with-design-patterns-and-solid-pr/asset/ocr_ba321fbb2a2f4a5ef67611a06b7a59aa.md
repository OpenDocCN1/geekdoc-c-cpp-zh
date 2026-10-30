```
```csharp
if (!tradeValidator.Validate(fields))
{
    continue;
}

var trade = tradeMapper.Map(fields);

trades.Add(trade);

lineCount++;
}
return trades;
}

private readonly ITradeValidator tradeValidator;
private readonly ITradeMapper tradeMapper;
}
```
```

The final refactor aims to abstract logging from two classes. Both the ITradeValidator and ITradeStorage implementations are still logging directly to the console. This time, instead of implementing your own logging class, you will create an adapter for the popular logging library, Log4Net. The UML class diagram in Figure 7-3 shows how this all fits together.

![](bbox=[0.158, 0.468, 0.7, 0.903])

**FIGURE 7-3** By implementing an adapter for Log4Net, you need not reference it in every assembly.