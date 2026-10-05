```
private void generateGraphData(byte[] data, int partitionStart, int partitionEnd,
ancellationToken token)
{
    for (int x = partitionStart; x < partitionEnd; x++)
    {
        for (double i = -p; i < p; i += 3)
        {
            // if (token.IsCancellationRequested)
            // return;
            // }
            token.ThrowIfCancellationRequested();
            ...
        }
    }
...}
```