To join enum values, you use a bitwise OR operator. To test for the existence of a particular bit, you use the bitwise AND operator. Both cases are illustrated in Listing 8.16.

# LISTING 8.16: Using Bitwise OR and AND with Flag Enums

```
using System;
using System.IO;

public class Program
{
    public static void Main()
    {
        // ...

        string fileName = @"enumtest.txt";

        System.IO.FileInfo file =
            new System.IO.FileInfo(fileName);

        file.Attributes = FileAttributes.Hidden |
            FileAttributes.ReadOnly;

        Console.WriteLine("{0} | {1} = {2}",
            FileAttributes.Hidden, FileAttributes.ReadOnly,
            (int)file.Attributes);

        if ((file.Attributes & FileAttributes.Hidden) !=
            FileAttributes.Hidden)
        {
            throw new Exception("File is not hidden.");
        }

        if ((file.Attributes & FileAttributes.ReadOnly) !=
            FileAttributes.ReadOnly)
        {
            throw new Exception("File is not read-only.");
        }

        // ...
    }
}
```

The results of Listing 8.16 appear in Output 8.5.

# OUTPUT 8.5

```
Hidden | ReadOnly = 3
```