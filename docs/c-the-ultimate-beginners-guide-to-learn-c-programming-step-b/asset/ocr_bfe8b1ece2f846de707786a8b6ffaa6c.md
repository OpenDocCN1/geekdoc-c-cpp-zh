+   - `public virtual bool ReadBoolean()-` for reading a Boolean value from the current stream and advancing the stream’s current position by a byte.
+   - `public virtual byte ReadByte()-` for reading the next byte from current stream into byte array and advancing current position by a similar number of bytes.

# BinaryWriter Class<sup>[45]</sup>

This class helps in writing binary data into a stream. To create a BinaryWriter object, we pass a FileStream object to the constructor. This class comes with a number of methods including the following:

+   - `public override void Close()-` for closing the BinaryWriter object as well as the underlying stream.
+   - `public virtual void Flush()-` this method will clear buffers for current writer and makes any buffered data to be written to the device.
+   - `public virtual void Write(bool value)-` for writing a one-byte Boolean value into the current stream. 1 represents true while 0 represents false.

Let us create an example that demonstrates how to read and write binary data:

```
```csharp
using System;
using System.IO;
namespace BinaryFileApplication {
    class MyProgram {
        static void Main(string[] args) {
            BinaryWriter bw;
            BinaryReader br;

            int x = 12;
            double db = 1.24658;
            bool bl = false;
            string st = "Hello world";

            //create a file
```
```