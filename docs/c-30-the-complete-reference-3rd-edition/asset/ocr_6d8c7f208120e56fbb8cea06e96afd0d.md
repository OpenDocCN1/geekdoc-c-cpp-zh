In the program, notice how inventory information is stored in its binary format. Thus, the number of items on hand and the cost is stored using their binary format rather than their human-readable text-based equivalents. This makes it is possible to perform computations on the numeric data without having to convert it from its human-readable form.

There is one other point of interest in the inventory program. Notice how the end of the file is detected. Since the binary input methods throw an EndOfStreamException when the end of the stream is reached, the program simply reads the file until either it finds the desired item or this exception is generated. Thus, no special mechanism is needed to detect the end of the file.

# Random Access Files

Up to this point, we have been using sequential files, which are files that are accessed in a strictly linear fashion, one byte after another. However, you can also access the contents of a file in random order. One way to do this is to use the Seek() method defined by FileStream. This method allows you to set the file position indicator (also called the file pointer or simply the current position) to any point within a file.

The method Seek() is shown here:

```
long Seek(long newPos, SeekOrigin origin)
```

Here, newPos specifies the new position, in bytes, of the file pointer from the location specified by origin. The origin will be one of these values, which are defined by the SeekOrigin enumeration:

| Value | Meaning |
|---|---|
| SeekOrigin.Begin | Seek from the beginning of the file. |
| SeekOrigin.Current | Seek from the current location. |
| SeekOrigin.End | Seek from the end of the file. |

After a call to Seek(), the next read or write operation will occur at the new file position. The new position is returned. If an error occurs while seeking, an IOException is thrown. If the underlying stream does not support position requests, a NotSupportedException is thrown. Other exceptions are possible.

Here is an example that demonstrates random access I/O. It writes the uppercase alphabet to a file and then reads it back in nonsequential order.

```
// Demonstrate random access.
using System;
using System.IO;

class RandomAccessDemo {
  static void Main() {
    FileStream f;
    char ch;
    try {
      f = new FileStream("random.dat", FileMode.Create);
    }

```