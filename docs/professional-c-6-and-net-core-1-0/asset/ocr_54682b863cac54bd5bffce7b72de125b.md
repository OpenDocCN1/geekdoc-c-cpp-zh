![](bbox=[0.105, 0.062, 0.893, 0.262])

# Figure 39.5

The major functionality of the client lies in the handler for the Click event of the Get Quote button:

```
protected async void OnGetQuote(object sender, RoutedEventArgs e)
{
    const int bufferSize = 1024;
    Cursor currentCursor = this.Cursor;
    this.Cursor = Cursors.Wait;
    quoteInfo.EnableRequest = false;

    string serverName = Properties.Settings.Default.ServerName;
    int port = Properties.Settings.Default.PortNumber;

    var client = new TcpClient();
    NetworkStream stream = null;
    try
    {
        await client.ConnectAsync(serverName, port);
        stream = client.GetStream();
        byte[] buffer = new byte[bufferSize];
        int received = await stream.ReadAsync(buffer, 0, bufferSize);
        if (received <= 0)
        {
            return;
        }
        quoteInfo.Quote =
Encoding.Unicode.GetString(buffer).Trim('\0');
    }
    catch (SocketException ex)
    {
        MessageBox.Show(ex.Message,"Error Quote of the day", MessageBoxButton.OK, MessageBoxImage.Error);
    }
    finally
    {
        stream?.Close();

        if (client.Connected)
        {
            client.Close();
        }
    }

    this.Cursor = currentCursor;
```