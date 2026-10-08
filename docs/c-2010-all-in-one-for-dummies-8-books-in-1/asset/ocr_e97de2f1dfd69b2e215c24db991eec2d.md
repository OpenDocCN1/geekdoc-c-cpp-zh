# Pulling Them Out of the Stream: Using StreamReader 449

```
if (sr == null) // Guard against trying to Close()a null object
{
    sr.Close(); // Takes care of flush as well
    sr = null;
}
```

```
// Wait for user to acknowledge the results.
Console.WriteLine("Press enter to terminate...");
Console.ReadLine();
```

```
// GetReaderFromFile Open the file and return a StreamReader for it.
private static StreamReader GetReaderForFile(string fileName)
```

```
StreamReader sr;
// Enter input filename.
Console.Write("Enter the name of a file to read:");
fileName = Console.ReadLine();
```

```
// User didn't enter anything; throw an exception
// to indicate that this is not acceptable.
if (fileName.Length == 0)
    throw new IOException("You need to enter a filename.");
```

```
// Got a name - open a file for reading; don't create the
// if it doesn't already exist.
FileStream fs = File.Open(fileName, FileMode.Open, FileAccess.Read);
```

```
// Wrap a StreamReader around the stream -- this will use
// the first three bytes of the file to indicate the
// encoding (but not the language).
sr = new StreamReader(fs, true);
return sr;
```

```
// Read one line at a time.
while(true)
{
    // Read a line.
    string input = sr.ReadLine();

    // Quit when you don't get anything.
    if (input == null)
    {
        break;
    }

    // Write whatever you read to the console.
    Console.WriteLine(input);
}
```

Book
Chapter 3

Fishing
FileStream