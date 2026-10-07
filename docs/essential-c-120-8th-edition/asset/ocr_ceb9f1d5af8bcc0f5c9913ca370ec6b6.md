# Main() Method

# DownloadDataAsyncTask()
Task

# ReadAsync() Tasks

Execution flows manually into
Main and up through the first
Console.WriteLine int;

```
Console.WriteLine(
"Searching for
file at URL " +
(url);
);
```

A call is made to
GetByteArrayAsync();
control flows into that method
as it would normally, still\sequentially:

```
Task[] data = await
HttpClient.
GetByteArrayAsync(
url);
Console.WriteLine(
"Loading..."
);
```

Once Task.Wait is
instantiated and queried,
returns to the Main()
while the task continues
to work.

```
GetByteArrayAsync(
Async());
```

With the await operator,
Main() method is allowed to
exhibit other methods while
await waits for completion.

```
HttpClient,
GetByteArrayAsync(url);
```

A call is made to
CountOccurrencesAsync();
so control flows into the
method as it would normally,
still executing in the
Main() method as shown.

```
byte[] data = await
task;
// GetByteArrayAsync()
completes
```

```
task = await Search
CountOccurrencesAsync(
data,
findText);
int textOccurrenceCount = 0;
```

The first instance of the do
loop occurs in the Main()
before switching to the
ReadAsync() related task.
Upon encountering an
vocation of ReadAsync()
normally a Task is
stantiated and awaited. It
returns to the caller while
the task continues
to work.

```
using Memory stream =
from(data);
/
// Loop 1
```

```
do // Loop 2 through n
length = await Read.ReadAsync(
data);
} while (length != 0)
```

With the next await operator,
Main() thread is allowed to
execute other workloads while
it waits for next
invocations of ReadAsync()
to complete and the caller
then receives the result
ofCountOccurrencesAsync()
to complete.

```
length =
await reader.ReadAsync(
data);
```

```
int textOccurrenceCount =
await task;
```

Upon completion, the result
is assigned to
textOccurrencesCount;.

```
while (length != 0)
True
False
```

Main() continues, writing out
the value of
textOccurrenceCount to
the console.

```
Console.WriteLine(
$(Environment.NewLine + findText) appears
(textOccurrenceCount) times at URL (url).");
```

```
return textOccurrenceCount;
// CountOccurrencesAsync()
completes
```

FIGURE 20.1: Flow control within each

![](bbox=[0.265, 0.098, 0.835, 0.818])