method.

# To modify the GraphDemo application to use an asynchronous method

+   1. Using Microsoft Visual Studio 2022, open the GraphDemo solution, which is located in the \Microsoft Press\VCSBS\Chapter 24\GraphDemo folder in your Documents folder.

+   2. In Solution Explorer, expand the MainPage.xaml and open the MainPage.xaml.cs file in the Code and Text Editor window.

+   3. In the MainPage class, locate the plotButton_Click method. The code in this method looks like this:

Click here to view code

```
private void plotButton_Click(object sender, RoutedEventArgs args)
{
    try
{
        Random rand = new Random();
        redValue = (byte)rand.Next(0xFF);
        greenValue = (byte)rand.Next(0xFF);
        blueValue = (byte)rand.Next(0xFF);
        tokenSource = new CancellationTokenSource();
        CancellationToken token = tokenSource.Token;

        int dataSize = bytesPerPixel * pixelWidth
        byte[] data = new byte[dataSize];

        Stopwatch watch = Stopwatch.StartNew();
try
{
    generateGraphData(data, 0, pixelWidth / 2, token);
    duration.Text = "$Duration (ms)";
watch.ElapsedMilliseconds)
}
catch (OperationCanceledException oce)
{
    duration.Text = oce.Message;
}
duration.Text = "$Duration (ms)";
```