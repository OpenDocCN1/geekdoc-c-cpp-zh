
```
enumerator.Dispose();
}
```

Then it prints:

```
1
2
Finally executed
```

View Demo

### Section 120.7: Eager evaluation

The **yield** keyword allows lazy-evaluation of the collection. Forcibly loading the whole collection into memory is called **eager evaluation**.

The following code shows this:

```
IEnumerable<int> myMethod()
{
    for(int i=0; i <= 8675309; i++)
    {
        yield return i;
    }
}
...
// define the iterator
var it = myMethod.Take(3);
// force its immediate evaluation
// list will contain 0, 1, 2
var list = it.ToList();
```

Calling ToList, ToDictionary or ToArray will force the immediate evaluation of the enumeration, retrieving all the elements into a collection.

### Section 120.8: Using yield to create an IEnumerator<T> when implementing IEnumerable<T>

The IEnumerable<T> interface has a single method, GetEnumerator(), which returns an IEnumerator<T>.

While the **yield** keyword can be used to directly create an IEnumerable<T>, it can also be used in exactly the same way to create an IEnumerator<T>. The only thing that changes is the return type of the method.

This can be useful if we want to create our own class which implements IEnumerable<T>:

```
public class PrintingEnumerable<T> : IEnumerable<T>
{
    private IEnumerable<T> _wrapped;

    public PrintingEnumerable(IEnumerable<T> wrapped)
    {
        _wrapped = wrapped;
    }

    // This method returns an IEnumerator<T>, rather than an IEnumerable<T>
    // But the yield syntax and usage is identical.
    public IEnumerator<T> GetEnumerator()
    {
        foreach(var item in _wrapped)
        {
            Console.WriteLine("Yielding: " + item);
            yield return item;
        }
    }

    IEnumerator IEnumerable.GetEnumerator()
    {
        return GetEnumerator();
    }
}
```

(Note that this particular example is just illustrative, and could be more cleanly implemented with a single iterator method returning an IEnumerable<T>.)

### Section 120.9: Lazy Evaluation Example: Fibonacci Numbers

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Numerics; // also add reference to System.Numerics

namespace ConsoleApplication33
{
    class Program
    {
        private static IEnumerable<BigInteger> Fibonacci()
        {
            BigInteger prev = 0;
            BigInteger current = 1;
            while (true)
            {
                yield return current;
                var next = prev + current;
                prev = current;
                current = next;
            }
        }

        static void Main()
        {
            // print Fibonacci numbers from 10001 to 10010
            var numbers = Fibonacci().Skip(10000).Take(10).ToArray();
            Console.WriteLine(string.Join(Environment.NewLine, numbers));
        }
    }
}
```

How it works under the hood (I recommend to decompile resulting .exe file in IL Disassembler tool):

- 1. C# compiler generates a class implementing IEnumerable<BigInteger> and IEnumerator<BigInteger> (<Fibonacci>d__0 in ildasm).
- 2. This class implements a state machine. State consists of current position in method and values of local variables.
- 3. The most interesting code are in bool IEnumerator.MoveNext() method. Basically, what MoveNext() do:

```
public static IEnumerable<int> Break()
{
    for (int i = 0; ; i++)
    {
        if (i < 10)
        {
            // Yields a number
            yield return i;
        }
        else
        {
            // Terminates just the loop
            break;
        }
    }
    // Execution continues
    yield return 10;
}
```

### Section 120.11: Return another Enumerable within a method returning Enumerable

```
public IEnumerable<int> F1()
{
    for (int i = 0; i < 3; i++)
        yield return i;

    //return F2(); // Compile Error!!
    foreach (var element in F2())
        yield return element;
}

public int[] F2()
{
    return new[] { 3, 4, 5 };
}
```

## Chapter 121: Task Parallel Library (TPL) Dataflow Constructs

### Section 121.1: ActionBlock<T>

(foreach)

This class can be thought of logically as a buffer for data to be processed combined with tasks for processing that data, with the "dataflow block" managing both. In its most basic usage, we can instantiate an ActionBlock and "post" data to it; the delegate provided at the ActionBlock's construction will be executed asynchronously for every piece of data posted.

![](img/5da9b5c72747b887ec63f57c832400bf_636_0.png)

#### Synchronous Computation

```
var ab = new ActionBlock<TInput>(i =>
{
    Compute(i);
});
...
ab.Post(1);
ab.Post(2);
ab.Post(3);
```

#### Throttling Asynchronous Downloads to at most 5 concurrently

```
var downloader = new ActionBlock<string>(async url =>
{
    byte [] imageData = await DownloadAsync(url);
    Process(imageData);
}, new DataflowBlockOptions { MaxDegreeOfParallelism = 5 });
downloader.Post("http://website.com/path/to/images");
downloader.Post("http://another-website.com/path/to/images");
```

Introduction to TPL Dataflow by Stephen Toub

### Section 121.2: BroadcastBlock<T>

(Copy an item and send the copies to every block that it's linked to)

Unlike BufferBlock, BroadcastBlock's mission in life is to enable all targets linked from the block to get a copy of every element published, continually overwriting the "current" value with those propagated to it.

Additionally, unlike BufferBlock, BroadcastBlock doesn't hold on to data unnecessarily. After a particular datum has been offered to all targets, that element will be overwritten by whatever piece of data is next in line (as with all dataflow blocks, messages are handled in FIFO order). That element will be offered to all targets, and so on.

![](img/5da9b5c72747b887ec63f57c832400bf_637_0.png)

#### Asynchronous Producer/Consumer with a Throttled Producer

```csharp
var ui = TaskScheduler.FromCurrentSynchronizationContext();
var bb = new BroadcastBlock<ImageData>(i => i);

var saveToDiskBlock = new ActionBlock<ImageData>(item =>
    item.Image.Save(item.Path)
);

var showInUiBlock = new ActionBlock<ImageData>(item =>
    imagePanel.AddImage(item.Image),
    new DataflowBlockOptions { TaskScheduler = TaskScheduler.FromCurrentSynchronizationContext() }
);

bb.LinkTo(saveToDiskBlock);
bb.LinkTo(showInUiBlock);
```

#### Exposing Status from an Agent

```csharp
public class MyAgent
{
    public ISourceBlock<string> Status { get; private set; }

    public MyAgent()
    {
        Status = new BroadcastBlock<string>();
        Run();
    }

    private void Run()
    {
        Status.Post("Starting");
        Status.Post("Doing cool stuff");
        ...
        Status.Post("Done");
    }
}
```

Introduction to TPL Dataflow by Stephen Toub

### Section 121.3: BufferBlock<T>

(FIFO Queue: The data that comes in is the data that goes out)

In short, BufferBlock provides an unbounded or bounded buffer for storing instances of T.
You can "post" instances of T to the block, which cause the data being posted to be stored in a first-in-first-out (FIFO) order by the block.
You can "receive" from the block, which allows you to synchronously or asynchronously obtain instances of T previously stored or available in the future (again, FIFO).

![](img/5da9b5c72747b887ec63f57c832400bf_638_0.png)

#### Asynchronous Producer/Consumer with a Throttled Producer

```csharp
// Hand-off through a bounded BufferBlock<T>
private static BufferBlock<int> _Buffer = new BufferBlock<int>(
    new DataflowBlockOptions { BoundedCapacity = 10 });

// Producer
private static async void Producer()
{
    while(true)
    {
        await _Buffer.SendAsync(Produce());
    }
}

// Consumer
private static async Task Consumer()
{
    while(true)
    {
        Process(await _Buffer.ReceiveAsync());
    }
}

// Start the Producer and Consumer
private static async Task Run()
{
    await Task.WhenAll(Producer(), Consumer());
}
```

Introduction to TPL Dataflow by Stephen Toub

### Section 121.4: JoinBlock<T1, T2,...>

(Collects 2-3 inputs and combines them into a Tuple)

Like BatchBlock, JoinBlock<T1, T2, ...> is able to group data from multiple data sources. In fact, that's JoinBlock<T1, T2, ...>'s primary purpose.

For example, a JoinBlock<string, double, int> is an ISourceBlock<Tuple<string, double, int>>.

As with BatchBlock, JoinBlock<T1, T2, ...> is capable of operating in both greedy and non-greedy mode.

- In the default greedy mode, all data offered to targets are accepted, even if the other target doesn't have the necessary data with which to form a tuple.
- In non-greedy mode, the block's targets will postpone data until all targets have been offered the necessary data to create a tuple, at which point the block will engage in a two-phase commit protocol to atomically retrieve all necessary items from the sources. This postponement makes it possible for another entity to consume the data in the meantime so as to allow the overall system to make forward progress.
