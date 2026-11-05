```
catch (InvalidDataException exc)
{
    Console.WriteLine(exc.Message);
}
catch (EndOfStreamException exc)
{
    Console.WriteLine(exc.Message);
}
catch (IOException exc)
{
    Console.WriteLine(exc.Message);
}
Console.ReadKey();
}

public static void RetrieveAndDisplayData(BinaryReader binReader)
{
    // Read string data from the file.
    Console.WriteLine(binReader.ReadString());

    // Read integer data from the file.
    for (int i = 0; i < 11; i++)
    {
        Console.WriteLine(binReader.ReadInt32());
    }

    // Read decimal data from the file.
    Console.WriteLine(binReader.ReadDecimal());
}
}
```

The code shown in Example 13-9 is used to retrieve the values that were stored in the binary file by the previous application, BinaryFiles. The code for BinaryFiles was displayed in Example 13-8. With Example 13-9, after the user enters the name of the file, objects of the FileStream and BinaryReader classes are instantiated. This is done inside a try...catch clause.

NOTE The file, BinaryInputTestFile.bin, created from Example 13-8 BinaryInput was moved to the bin/Debug directory for this application. If you do not specify the full path where the file is located, the application looks in the bin/Debug directory.