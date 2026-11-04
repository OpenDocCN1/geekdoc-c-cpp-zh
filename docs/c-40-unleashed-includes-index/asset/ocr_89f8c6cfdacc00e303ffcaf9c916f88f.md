as we're passing the constant value 1 as an object to the Add method). When reading from the list using indexer syntax, we must cast the retrieved object back to the Int32 value type, something we expect to cause unboxing.

The PrintGCStats method uses the System.GC class to query the garbage collector for statistics about the number of collections carried out so far during the runtime of the program, on a per-generation basis. (See earlier chapters in this book for more information about this.)

```
static void PrintGCStats() {
    Console.WriteLine("Gen 0: {0}, Gen 1: {1}, Gen 2: {2}\n",
        GC.CollectionCount(1), GC.CollectionCount(2), GC.CollectionCount(3));
}
```

Next, we do the same for the generic List<int> type. For this case, we expect things to be better because the storage array will get strongly typed at runtime when the CLR creates a specialized constructed generic type:

```
Measure("Write List<int>: {0}", () => {
    for (int i = 0; i < N; i++)
        genList.Add(1); // Expected: capacity check
});
Measure("Read List<int>: {0}", () => {
    int sum = 0;
    for (int i = 0; i < N; i++)
        sum += genList[i];
});
PrintGCStats();
```

Notice how the read loop no longer needs a cast expression because the indexer on the generic list object will be statically typed to produce an int value.

Finally, to establish a basis for comparisons, we apply the same tests to a plain int array, which we expect to get the best performance across the board. After all, each of the collection types we're testing encapsulates an array:

```
Measure("Write int array: {0}", () => {
    for (int i = 0; i < N; i++)
        array[i] = 1;
});
Measure("Read int array: {0}", () => {
    int sum = 0;
    for (int i = 0; i < N; i++)
        sum += array[i];
});
PrintGCStats();
```