work message, it invokes the code following the await call. (As a result, the invocation of the continuation code is on the same thread as the caller that processed the message pump.)

There is a key code readability feature built into the TAP language pattern. Notice in Listing 18.22 that the call to return pingReply.Status appears to flow naturally after the await, providing a clear indication that it will execute immediately following the previous line. However, writing what really happens from scratch would be far less understandable for multiple reasons.

# await Operators

There is no limitation on the number of times that await can be placed into a single method. In fact, such statements are not limited to appearing one after another. Rather, await statements can be placed into loops and processed consecutively one after the other, thereby following a natural control flow the way code appears. Consider the example in Listing 18.23.

# LISTING 18.23: Iterating over an Await Operation

```
async private void PingButton_Click(
    object sender, RoutedEventArgs e)
{
    List<string> urls = new List<string>()
    {
        "www.habitat-spokane.org",
        "www.partnersintl.org",
        "www.iassist.org",
        "www.fh.org",
        "www.worldvision.org"
    };
    IPStatus status;

    Func<string, Task<IPStatus>> func =
        async (localUrl) =>
        {
            Ping ping = new Ping();
            PingReply pingReply =
                await ping.SendPingAsync(localUrl);
            return pingReply.Status;
        };

    StatusLabel.Content = "Pinging..";

    foreach(string url in urls)
    {
        status = await func(url);
    }
```