Each thread picks up one record from the database, and processes the partial result locally in the thread. When a thread finishes its job (that is, there are no more records to process), it merges the partial result into the aggregated one.

![](bbox=[0.101, 0.183, 0.153, 0.246])

# LISTING 10-9: Parallel Query Implemented Manually

```
private Iumerable<LIResult> ManualParallelQuery(string wordToSearch)
{
    var result = new Dictionary<int, LIResult>();
    int partitionsCount = Environment.ProcessorCount;
    int remainingCount = partitionsCount;
    IEnumerable<LIRecord> enumerator = LIRecords.GetEnumerator();
    // Resource block for enumerator
    try {
        // Synchronization of partitions
        using (var done = new ManualResetEvent(false))
            // Each partition has its own thread
            for (int i = 0; i < partitionsCount; i++)
            ThreadPool.QueueUserItem((obj) => {
                var partialResult = new Dictionary<int, LIResult>();
                while (true)
                    LIRecord record;
                    // Lock (inefficient) to access the next element
                    lock (enumerator)
                        if (!enumerator.MoveNext()) break;
                        record = enumerator.Current;
                    if (String.Compare(record.Word, wordToSearch, true) == 0)
                        LIResult book;
                        // Lock (inefficient) to aggregate result
                        lock (partialResult)
                            if (partialResult.TryGetValue(record.Book, out book))
                                book.WordCount++;
                            else
                                partialResult.Add(record.Book,
                                    new LIResult(record.Book, 1));
                });
    }
    // Merge partial result to the aggregated result
    lock (result)
```