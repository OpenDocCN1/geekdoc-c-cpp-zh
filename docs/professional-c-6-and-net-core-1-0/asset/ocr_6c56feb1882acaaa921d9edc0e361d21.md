```
stage 3: added DisplayBits
stage 3: added bits2
stage 3: added Write
stage 3: added =
stage 3: added bits1.Or
stage 2: added             DisplayBits(bits2);
stage 2: added             Write(" and");
stage 2: added             DisplayBits(bits1);
stage 2: added             WriteLine();
stage 2: added             DisplayBits(bits2);
```

# Completing the Pipeline

After the first three stages are completed, the next three stages can run in parallel again. TransferContentAsync gets the data from the dictionary, converts it to the type Info, and puts it into the output BlockingCollection<T> (code file PipelineSample/PipelineStages.cs):

```
public static Task TransferContentAsync(
    ConcurrentDictionary<string, int> input,
    BlockingCollection<Info> output)
{
    return Task.Factory.StartNew(() =>
    {
        foreach (var word in input.Keys)
        {
            int value;
            if (input.TryGetValue(word, out value))
            {
                var info = new Info { Word = word, Count = value };
                output.Add(info);
                ColoredConsole.WriteLine($"stage 4: added {info}");
            }
        }
        output.CompleteAdding();
    }, TaskCreationOptions.LongRunning);
}
```

The pipeline stage AddColorAsync sets the Color property of the Info type depending on the value of the Count property:

```
public static Task AddColorAsync(BlockingCollection<Info> input,
    BlockingCollection<Info> output)
{
    return Task.Factory.StartNew(() =>
    {
        foreach (var item in input.GetConsumingEnumerable())
        {
            if (item.Count > 40)
            {
                item.Color ="Red";
            }
            else if (item.Count > 20)
            {
                item.Color ="Yellow";
            }
            else
            {
                item.Color ="Green";
            }
            output.Add(item);
            ColoredConsole.WriteLine($"stage 5: added color {item.Color} to {item}");

```