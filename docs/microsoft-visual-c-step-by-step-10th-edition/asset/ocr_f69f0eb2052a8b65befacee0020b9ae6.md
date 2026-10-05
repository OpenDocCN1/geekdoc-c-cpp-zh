```
private async void plotButton_Click(object sender, RoutedEventArgs e)
{
    try
    {
        await first;
        await second;
        duration.Text = $"Duration (ms): {watch.ElapsedMilliseconds}";
    }
    catch (OperationCanceledException oce)
    {
        duration.Text = oce.Message;
    }
    string message = $"Status of tasks is {first.Status}, {second.Status}";
}
```