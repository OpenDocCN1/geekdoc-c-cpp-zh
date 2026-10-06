# Understanding Streams

```
using System.Console;
using System.IO;
class WriteSomeText
{
    static void Main()
    {
        FileStream outFile = new
FileStream("SomeText.txt", FileMode.Create,
FileAccess.Write);
        StreamWriter writer = new StreamWriter(outFile);
        Write("Enter some text >>");
        string text = ReadLine();
        writer.WriteLine(text);
        // Error occurs if the next two statements are reversed
        writer.Close();
        outFile.Close();
    }
}
```

**Figure 14-7** The WriteSomeText program

Although the WriteSomeText application uses ReadLine() to accept user input, you could also create
a GUI Form to accept input. You will create an application that writes to and reads files using a GUI
environment in a "You Do It" exercise at the end of this chapter.

```
Enter some text >> There's no place like home.
```

**Figure 14-8** Typical execution of the WriteSomeText program

![](bbox=[0.104, 0.677, 0.476, 0.793])

**Figure 14-9** File created by the WriteSomeText program

In applications that use files, you will want to make all the statements that open, write to, read from,and close files in a try block and catch any IOExceptions that are thrown. Exception handling is
elinated from many examples in this chapter so that you can concentrate on the details of handling files
without extra statements. In the "You Do It" section at the end of this chapter, you will add exception handling
to an application.

Copyright 2018 Cengage Learning. All Rights Reserved. May not be copied, scanned, or duplicated, in whole or in part. WCN 022-200-292