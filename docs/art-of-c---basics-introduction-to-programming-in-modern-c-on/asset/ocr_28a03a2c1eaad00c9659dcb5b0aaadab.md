stock-ticker/Program.cs

```
using Exchange;

const int intervalMillis = 500;

var symbols = new[] { Prices.AAPL, Prices.MSFT };

var stocks = new Dictionary<string, Stock>() {
    { Prices.AAPL, new(Prices.AAPL, 0.0m) },
    { Prices.MSFT, new(Prices.MSFT, 0.0m) },
};

while (true) {
    foreach (var symbol in symbols) {
        var stock = Ticker.Get(symbol);
        if (stock != stocks[symbol]) {
            stocks[symbol] = stock;
            Console.WriteLine(stock);
        }
    }

    await Task.Delay(intervalMillis);
}
```