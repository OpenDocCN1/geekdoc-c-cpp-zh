```
using (var outputStream = File.OpenWrite(outputFile))
{
    inputStream.CopyTo(outputStream);
}
}
```

# Using Random Access to Streams

Random access to streams provides an advantage in that—even with large files—you can access a specific position within the file in a fast way.

To see random access in action, the following code snippet creates a large file. This code snippet creates the file sampleddata.data with records that are all the same length and contain a number, a text, and a random date. The number of records that is passed to the method is created with the help of the Enumerable.Range method. The Select method creates an anonymous type that contains Number, Text, and Date properties. Out of these records, a string with # pre- and postfix is created, with a fixed length for every value and a ; separator between each value. The WriteAsync method writes the record to the stream (code file StreamSamples/Program.cs):

```
const string SampleFilePath = "./samplefile.data";

public static async Task CreateSampleFile(int nRecords)
{
    FileStream stream = File.Create(SampleFilePath);
    using (var writer = new StreamWriter(stream))
    {
        var r = new Random();

        var records = Enumerable.Range(0, nRecords).Select(x => new
        {
            Number = x,
            Text = $"Sample text {r.Next(200)}",
            Date = new DateTime(Math.Abs((long)((r.NextDouble() * 2 - 1) * DateTime.MaxValue.Ticks)))
        });

        foreach (var rec in records)
        {
            string date = rec.Date.ToString("d", CultureInfo.InvariantCulture);
            string s =
                $"#{rec.Number,8};{rec.Text,-20};{date}#\n";
            await writer.WriteAsync(s);
        }
    }
}
```