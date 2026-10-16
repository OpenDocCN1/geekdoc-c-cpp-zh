```
bool completed = false;
do
{
    byte[] readBuffer = new byte[1024];
    int read = await stream.ReadAsync(
        readBuffer, 0, readBuffer.Length);
    string request =
Encoding.ASCII.GetString(readBuffer, 0, read);
    WriteLine($"received {request}");

    string sessionId;
    string result;
    byte[] writeBuffer = null;
    string response = string.Empty;

    ParseResponse resp = ParseRequest(
        request, out sessionId, out result);
    switch (resp)
    {
        case ParseResponse.OK:
            string content = $"{STATUSOK}::{SESSIONID}::
{sessionId}";
            if (!string.IsNullOrEmpty(result))
            {
                content += $"{SEPARATOR}{result}";
            }
            response = $"{STATUSOK}{SEPARATOR}{SESSIONID}
{SEPARATOR}" +
                $"{sessionId}{SEPARATOR}{content}";
            break;
        case ParseResponse.CLOSE:
            response = $"{STATUSCLOSED}";
            completed = true;
            break;
        case ParseResponse.TIMEOUT:
            response = $"{STATUSTIMEOUT}";
            break;
        case ParseResponse.ERROR:
            response = $"{STATUSINVALID}";
            break;
        default:
            break;
    }
    writeBuffer = Encoding.ASCII.GetBytes(response);
    await stream.WriteAsync(writeBuffer, 0,
writeBuffer.Length);
    await stream.FlushAsync();
    WriteLine($"returned {Encoding.ASCII.GetString(
        writeBuffer, 0, writeBuffer.Length)}");
    } while (!completed);
}
}
}
catch (Exception ex)
{
    WriteLine($"Exception in client request handling" +
        "of type {ex.GetType().Name}, Message: {ex.Message}");
}
WriteLine("client disconnected");
});
}
```

The ParseRequest method parses the request and filters out the session identifier. The first call to the server (HELO) is the only call where a