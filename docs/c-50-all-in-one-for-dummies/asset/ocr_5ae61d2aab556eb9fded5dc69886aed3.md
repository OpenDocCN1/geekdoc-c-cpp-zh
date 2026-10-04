# 448 StreamWriting for Old Walter

```
FileMode.Create,
FileAccess.Write);

// Pass the fs variable to the StreamWriter in the using statement.
using (StreamWriter sw = new StreamWriter(fs))
{
    // sw exists only within the block, which is a local scope.

    // Read one string at a time from the console, outputting each to the
    // FileStream for writing.
    Console.WriteLine("Enter text; enter blank line to stop");
    while (true)
    {
        // Read next line from Console; quit if line is blank.
        string input = Console.ReadLine();
        if (input == null)
        {
            break;
        }
        // Write the line just read to output file via the stream.
        sw.WriteLine(input);
    }
    // Loop back to get another line and fs is now closed.
fs = null; // Make sure you don't access fs again.
```

The items after the using keyword are your "resource acquisition" section, where you allocate one or more resources as streams, readers/writers, fonts, and so on. (If you allocate more than one resource, they have to be of the same type.) Following that section is the enclosing block, bounded by the outer braces.

> The statement block is not a loop. The block only defines a scope, like the try block or a method's block. (Variables defined within the block, its head, don't exist outside the block. Thus the StreamWriter sw isn't visible outside the using block.) I discuss scope in I.

At the top of the example, in the resource-acquisition section, you set up a resource — in this case, create a new StreamWriter wrapped around the already-existing FileStream Inside the block is where you carry out your i/o code for the file.

At the end of the using block, C# automatically flushes the StreamWriter, closes it, and closes the FileStream, also flushing any bytes it still contains to the disk. Ending the using block also disposes the StreamWriter object—see the warning and technical discussion coming up.

It's a good practice to work most with streams in using statements. Wrapping the StreamWriter or StreamReader in a using statement, for example, has the same effect as using the writer or reader in a try/finally exception-handling block. (See Block I for it exceptions.) In fact, the compiler translates the block into the same code it uses for a try/finally, which guarantees that the resources get cleaned up:

![](bbox=[0.14, 0.565, 0.235, 0.735])