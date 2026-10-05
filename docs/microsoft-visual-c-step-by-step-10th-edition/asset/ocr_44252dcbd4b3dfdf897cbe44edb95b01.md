```
private void plotButton_Click(object sender, RoutedEventArgs e)
{
```

```
Random rand = new Random();
readValue = (byte)rand.Next(0xFF);
greenValue = (byte)rand.Next(0xFF);
blueValue = (byte)rand.Next(0xFF);
```

```
tokenSource = new CancellationTokenSource();
CancellationToken token = tokenSource.Token;
```

```
}
```