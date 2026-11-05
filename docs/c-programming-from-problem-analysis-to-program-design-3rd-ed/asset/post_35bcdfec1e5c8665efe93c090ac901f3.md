
The `BinaryReader` and `BinaryWriter` classes offer streaming functionality that is oriented toward particular data types. As you review the `BinaryReader` methods shown in Table 13-8, you will notice several `Read( )` methods. Each is focused on the type of data that it would be retrieving from a file.

**Table 13-8 BinaryReader members**

| Method | Description |
|---|---|
| `Close( )` | Closes the current BinaryReader and the underlying stream |
| `PeekChar( )` | Returns the next available character and does not advance the byte or character position |
| `Read( )` | Reads characters from the underlying stream and advances the current position of the stream |
| `ReadBoolean( )` | Reads a Boolean value from the current stream and advances the current position of the stream by 1 byte |
| `ReadByte( )` | Reads the next byte from the current stream and advances the current position of the stream by 1 byte |
| `ReadBytes( )` | Reads count bytes from the current stream into a byte array and advances the current position by count bytes |
| `ReadChar( )` | Reads the next character from the current stream and advances the current position of the stream |
| `ReadChars( )` | Reads count characters from the current stream, returns the data in a character array, and advances the current position |
| `ReadDecimal( )` | Reads a decimal value from the current stream and advances the current position of the stream by 16 bytes |
| `ReadDouble( )` | Reads an 8-byte floating-point value from the current stream and advances the current position of the stream by 8 bytes |
| `ReadInt32( )` | Reads a 4-byte signed integer from the current stream and advances the current position of the stream by 4 bytes |
| `ReadString( )` | Reads a string from the current stream; the string is prefixed with the length |

Example 13-8 illustrates using the `BinaryWriter` class to create a binary file that stores integers, decimals, and string data types.

### Example 13-8

```csharp
// BinaryFiles.cs
// Illustrates creating a binary file
using System;
using System.Collections.Generic;
using System.Text;
using System.IO;

namespace BinaryFiles
{
    class BinaryExample
    {
        public static void Main( )
        {
            FileStream filStream;
            BinaryWriter binWriter;

            Console.Write("Enter name of the file: ");
            string fileName = Console.ReadLine( );
            if (File.Exists(fileName))
            {
                Console.WriteLine("File - {0} already exists!",
                                  fileName);
            }
            else
            {
                filStream = new FileStream(fileName,
                                           FileMode.CreateNew);
                binWriter = new BinaryWriter(filStream);
                decimal aValue = 2.16M;

                binWriter.Write("Sample Run");
                for (int i = 0; i < 11; i++)
                {
                    binWriter.Write(i);
                }
                binWriter.Write(aValue);

                binWriter.Close( );
                filStream.Close( );
                Console.WriteLine("File Created successfully");
            }
            Console.ReadLine( );
        }
    }
}
```

Example 13-8 first checks to see if the filename entered by the user already exists. This is accomplished using the **static Exists()** method of the **File** class. When the name entered is a new file, objects are instantiated of the **FileStream** and **BinaryWriter** classes. Notice that the second argument to the **FileStream** constructor is an enumeration. The **FileMode** enumerated type specifies how the operating system should open the file. As shown in Figure 13-10, the field value member named **CreateNew** indicates that the operating system should create a new file. IntelliSense notes that the **System.IO.IOException** is thrown if the file already exists.

![](img/e33ae760e23d89eac66541252ad65de8_837_0.png)

**Figure 13-10** Enumerated FileMode

The **BinaryWriter object** is based on the **FileStream object** or wrapped around the **FileStream object**. The **FileStream object** is sent in as an argument to the **BinaryWriter** constructor.

In Example 13-8, first a string argument is written to the file. This is followed by several integers and a decimal value. Finally, for the file to be created properly, both files must be closed. Figure 13-11 shows the console output produced. In the foreground of the figure, you see the newly created file.

![](img/e33ae760e23d89eac66541252ad65de8_838_0.png)

**Figure 13-11** TestBinaryCreation.txt file created

As you can see from Figure 13-11, because no path was specified, the file is stored in the `bin\debug` directory for the project.

After a binary file is created, you cannot simply open the file in Notepad and view its contents. If you do, you will find a number of nonprintable characters. You can write program statements that use the **BinaryReader** class to retrieve the results. This is illustrated in Example 13-9.

### Example 13-9

```csharp
// BinaryFileAccess.cs
// Illustrates retrieving data from a binary file.

using System;
using System.Collections.Generic;
using System.Text;
using System.IO;

namespace BinaryFileAccess
{
    class BinaryInput
    {
        public static void Main( )
        {
            FileStream filStream;
            BinaryReader binReader;

            Console.Write("Enter name of the file: ");
            string fileName = Console.ReadLine( );
            try
            {
                filStream = new FileStream(fileName, FileMode.Open,
                                            FileAccess.Read);
                binReader = new BinaryReader(filStream);

                RetrieveAndDisplayData(binReader);

                binReader.Close( );
                filStream.Close( );
            }
            catch (FileNotFoundException exc)
            {
                Console.WriteLine(exc.Message);
            }
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
            Console.ReadLine( );
        }

        public static void RetrieveAndDisplayData(BinaryReader binReader)
        {
            // Read string data from the file.
            Console.WriteLine(binReader.ReadString( ));
            // Read integer data from the file.
            for (int i = 0; i < 11; i++)
            {
                Console.WriteLine(binReader.ReadInt32( ));
            }
            // Read decimal data from the file.
            Console.WriteLine(binReader.ReadDecimal( ));
        }
    }
}
```

The code shown in Example 13-9 is used to retrieve the values that were stored in the binary file by the previous application, BinaryFiles. The code for BinaryFiles was displayed in Example 13-8. With Example 13-9, after the user enters the name of the file, objects of the FileStream and BinaryReader classes are instantiated. This is done inside a try...catch clause. The constructor for the FileStream object includes values for two enumerated types (FileMode.Open and FileAccess.Read). Figure 13-12 shows the output produced from the run.

![](img/e33ae760e23d89eac66541252ad65de8_840_0.png)

**Figure 13-12** Reading string, integer, and decimal data from a binary file

Three different methods were invoked to read data from the file. The ReadInt32( ) method retrieved the 10 integers. The ReadDecimal( ) reads the decimal value placed in the file, and the ReadString( ) was invoked to retrieve the string value. You might wonder how it knew to retrieve only the alphabetic characters "Sample Run" when the ReadString( ) method was called. The ReadString( ) method is the first method invoked. As shown in Table 13-8, strings are prefixed with a length when they are stored in the file. The ReadString( ) method uses that value to determine how many characters to retrieve. Several catch clauses were included. All derived classes of the IOException were placed prior to the IOException catch because the order of placement is important.
