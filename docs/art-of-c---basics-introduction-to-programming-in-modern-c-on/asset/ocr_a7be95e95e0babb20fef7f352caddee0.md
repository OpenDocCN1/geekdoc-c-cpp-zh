```
}

public async Task Run() {
    var tasks = new List<Task>();
    foreach (var (r, h) in handlers) {
        if (r.Length > 0) {
            var t = Listener.StartAsync(r, h);
            tasks.Add(t);
        }
    }

    await Task.WhenAll(tasks);
}
```

```
private async Task ProcessTextResponse(HttpListenerContext ctx) {
    byte[] data = Encoding.UTF8.GetBytes(TextMessage);
    ctx.Response.ContentLength64 = data.Length;

    using var stream = ctx.Response.OutputStream;
    stream.Write(data, 0, data.Length);
    stream.Flush();
    stream.Close();

    await Task.Delay(1);
    Console.WriteLine($"Responded at {DateTime.Now}");
}
```

```
private async Task ProcessJsonResponse(HttpListenerContext ctx) {
    string json = JsonSerializer.Serialize(JsonPayload);
    byte[] data = Encoding.UTF8.GetBytes(json);

    var response = ctx.Response;
    response.ContentType = "application/json";
    response.ContentLength64 = data.Length;

    using var stream = response.OutputStream;
    stream.Write(data, 0, data.Length);
    stream.Flush();
    stream.Close();
```