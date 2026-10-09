A "server" is mainly about behavior. A server serves. It processes. It otherwise does something. A server is a class.

We use a small static method to encapsulate the logic of starting an instance of System.Net.HttpLister.

*web-server-simple/Listener.cs (lines 4-19)*

```
4 static class Listener {
5 internal static async Task StartAsync(string[] prefixes, Func<HttpListenerContext, Task> handler) {
6 using var listener = new HttpListener();
7 foreach (string s in prefixes) {
8 listener.Prefixes.Add(s);
9 }
10
11 listener.Start();
12 Console.WriteLine($"Listening on {{{string.Join(", ", prefixes)}}}");
13
14 while (true) {
15 var context = await listener.GetContextAsync();
16 await handler(context);
17 }
18 }
19}
```

# ## 24.3. Pair Programming - Async Programming, Func Delegates, HttpListener, JsonSerializer

Because of the importance of Web programming, most programming languages and runtimes have a very good support for creating a simple Web server.