```
public int ServerPort
{
    get { return _serverPort; }
    set { SetProperty(ref _serverPort, value); }
}

private string _sessionId;
public string SessionId
{
    get { return _sessionId; }
    set { SetProperty(ref _sessionId, value); }
}

private CustomProtocolCommand _activeCommand;
public CustomProtocolCommand ActiveCommand
{
    get { return _activeCommand; }
    set { SetProperty(ref _activeCommand, value); }
}

private string _log;
public string Log
{
    get { return _log; }
    set { SetProperty(ref _log, value); }
}

private string _status;
public string Status
{
    get { return _status; }
    set { SetProperty(ref _status, value); }
}
//...
}
```

The method OnConnect is called when the user clicks the Connect button. The connection to the TCP server is made, invoking the ConnectAsync method of the TcpClient class. In case the connection is in a stale mode, and the OnConnect method is invoked once more, a SocketException is thrown where the ErrorCode is set to 0x2748. A C# 6 exception filter is used here to handle this case of the SocketException and create a new TcpClient, so invoking OnConnect once more likely succeeds:

```
private async void OnConnect(object sender, RoutedEventArgs e)
{
    try
    {
        await _client.ConnectAsync(RemoteHost, ServerPort);
    }
    catch (SocketException ex) when (ex.ErrorCode == 0x2748)
    {
        _client.Close();
        _client = new TcpClient();
        MessageBox.Show("please retry connect");
    }
    catch (Exception ex)
    {
        MessageBox.Show(ex.Message);
    }
}
```