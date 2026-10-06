```
ignore < queue.CreateIfNotNotExist()
ignore < queue.CreateIfNotNotExist()
```

```
let data = [ | 1..100 |]
```

```
// map step, split the data into small chunks
let chunk = 9
// insert 10 elements
[0..chunk]
|> Seq.map(fun i -> i * 10, (i + 1) * 10 - 1)
|> Seq.iter(fun (a,b) ->
    let l =
    data.[a..b]
    |> Array.map(fun i -> i.ToString())

queue.AddMessage(CloudQueueMessage(String.Join(", ", l)))
```

```
// reduce step, retrieve message and sum
let result =
[0..chunk]
|> Seq.map(fun _ ->n    while queue.PeekMessage() = null do
        Thread.Sleep(random.Next(5, 100))
    queue.GetMessage().AsString |> Convert.ToInt32)
 Seq.sum
```

```
log (printf "final result = %A" result "Information")
```

```
log "MasterNode entry point called "Information"
while(true) do
    Thread.Sleep(10000)
    log "Working" "Information"
```

```
override wr.OnStart() =
```

```
// Set the maximum number of concurrent connections
ServicePoint.DefaultConnectionLimit <= 12
```

```
// For information on handling configuration changes
// see the MSDN topic at http://go.microsoft.com/fwlink/?LinkId=166357.
```

```
base.OnStart()
```

> Note The queue name cannot have uppercase characters.

The worker node, which is relatively simple, is shown in Listing 8-13. It takes the data from the queue, which is queue1, and performs a Seq.sum operation. The summary result is inserted into the result queue, which is queue2.