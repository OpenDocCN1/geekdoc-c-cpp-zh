```
const byte ToSearch = 123;
byte[][] DumpInfo = new byte[ByteSeries][];
```

```
Parallel.For(0, ByteSeries, index =>
{
    var blob = new byte[BlobSize];
    new Random((int)DateTime.Now.Ticks).NextBytes(blob);
    lock (DumpInfo) { DumpInfo[index] = blob; }
});
```

```
Parallel.For(0, ByteSeries, (index, state) =>
{
    if (state.ShouldExitCurrentIteration) return;

    Console.WriteLine("Search in #{0}", index);
    foreach (byte b in DumpInfo[index])
    {
        if (b == ToSearch)
        {
            Console.WriteLine("Halt request in #{0}", index);
            state.Stop();
            break;
        }
    }
    Console.WriteLine("Press Enter to exit...");
    Console.ReadLine();
});
```

Code file [Program.cs] available for download at Wrox.com

The DumpInfo two-dimensional array holds 100,000 bytes, each of having a size of 100 bytes. The first Parallel.For initializes the bytes with random bytes, and this loop does not use ParallelLoopState. The second Parallel.For iterates through loops and searches for a byte with a value of 123. In the iteration body, state represents the ParallelLoopState instance. When 123 is found, the Stop method signals the loop to be halted. Because, at the entry of the body the ShouldExitCurrentIteration property is checked, any iteration bodies starting after Stop will immediately return without searching the blob. Figure 10-15 shows an output of this example.

![](bbox=[0.147, 0.775, 0.798, 0.893])

Figure 10-15: Output of the Parallel.For example