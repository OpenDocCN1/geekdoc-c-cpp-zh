```
private async void plotButton_Click(object sender, RoutedEventArgs e)
{
```

```
tokenSource = new CancellationTokenSource();
CancellationToken token = tokenSource.Token;
```

```
Task first = Task.Run(() => generateGraphData(data, 0, pixelWidth / 4, token));
Task second = Task.Run(() => generateGraphData(data, pixelWidth / 2, token));
```

```
}
```

+   2. Add a block around the statements that run the tasks, wait for them to complete, and display the elapsed time. Then add a catch block that handles the OperationCanceledException. In this exception handler, display the reason for the exception reported in the Message property of the exception object in the duration TextBlock control. The following code shown in bold highlights the changes you should make:

Click here to view code image

```
private async void plotButton_Click(object sender, RoutedEventArgs e)
{
```

```
try {
    await first;
    await second;
duration.Text = $"Duration (ms): {watch.ElapsedMilliseconds}";
}
```

```
catch (OperationCanceledException oce) {
    duration.Text = oce.Message;
}
string message = $"Status of tasks is {first.Status}, {second.Status}";
```

```
}
```

+   3. In the generateGraphData method, comment out the if statement that examines the IsCancellationRequested property of the CancellationToken object and