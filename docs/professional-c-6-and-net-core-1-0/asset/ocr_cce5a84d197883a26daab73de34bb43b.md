![](bbox=[0.1, 0.06, 0.9, 0.29])

# Figure 23.3

As far as reading and writing files goes, the classes that concern us most are the following:

+   - `FileStream`—This class is intended for reading and writing binary data in a file.
+   - `StreamReader` and `StreamWriter`—These classes are designed specifically for reading from and writing to streams offering APIs for text formats.
+   - `BinaryReader` and `BinaryWriter`—These classes are designed for reading and writing to streams offering APIs for binary data.

The difference between using these classes and directly using the underlying stream objects is that a basic stream works in bytes. For example, suppose that as part of the process of saving some document you want to write the contents of a variable of type `long` to a binary file. Each `long` occupies 8 bytes, and if you use an ordinary binary stream you would have to explicitly write each of those 8 bytes of memory.

In C# code, you would have to perform some bitwise operations to extract each of those 8 bytes from the `long` value. Using a `BinaryWriter` instance, you can encapsulate the entire operation in an overload of the `BinaryWriter.Write` method, which takes a `long` as a parameter, and which places those 8 bytes into the stream (and if the stream is directed to a file, into the file). A corresponding `BinaryReader.Read` method extracts 8 bytes from the stream and recovers the value of the `long`.

# Working with File Streams

Let’s get into programming streams reading and writing files. A `FileStream` instance is used to read or write data to or from a file. To construct a `FileStream`, you need four pieces of information:

+   1. The *file* you want to access.
+   2. The *mode*, which indicates how you want to open the file. For example, are you intending to create a new file or open an existing