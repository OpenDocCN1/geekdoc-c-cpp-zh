
`get(byte[] bytes)` and `get(byte[], int offset, int length)`

Finally, there are methods `getInt`, `getLong`, `getShort`, `getChar`, `getFloat`, `getDouble` to read primitive type values that are stored as *binary* values in the file. As we already mentioned, Java uses big-endian ordering for binary data. However, if you need to process a file containing binary numbers in little-endian order, simply call

`buffer.order(ByteOrder.LITTLE_ENDIAN);`

To find out the current byte order of a buffer, call

`ByteOrder b = buffer.order();`

> **CAUTION:** This pair of methods does not use the set/get naming convention.

To write numbers to a buffer, use one of the methods `putInt`, `putLong`, `putShort`, `putChar`, `putFloat`, `putDouble`.

At some point, and certainly when the channel is closed, these changes are written back to the file.

Listing 2.5 computes the 32-bit cyclic redundancy check (CRC32) of a file. That checksum is often used to determine whether a file has been corrupted. Corruption of a file makes it very likely that the checksum has changed. The `java.util.zip` package contains a class `CRC32` that computes the checksum of a sequence of bytes, using the following loop:

```java
CRC32 crc = new CRC32();
while (more bytes)
    crc.update(next byte)
long checksum = crc.getValue();
```

## Listing 2.5 *(Continued)*

```java
CRC32 crc = new CRC32();
int c;
while ((c = in.read()) != -1)
    crc.update(c);
return crc.getValue();
}
}

public static long checksumRandomAccessFile(Path filename) throws IOException
{
    try (RandomAccessFile file = new RandomAccessFile(filename.toFile(), "r"))
    {
        long length = file.length();
        CRC32 crc = new CRC32();

        for (long p = 0; p < length; p++)
        {
            file.seek(p);
            int c = file.readByte();
            crc.update(c);
        }
        return crc.getValue();
    }
}

public static long checksumMappedFile(Path filename) throws IOException
{
    try (FileChannel channel = FileChannel.open(filename))
    {
        CRC32 crc = new CRC32();
        int length = (int) channel.size();
        MappedByteBuffer buffer = channel.map(FileChannel.MapMode.READ_ONLY, 0, length);

        for (int p = 0; p < length; p++)
        {
            int c = buffer.get(p);
            crc.update(c);
        }
        return crc.getValue();
    }
}

public static void main(String[] args) throws IOException
{
    System.out.println("Input Stream:");
    long start = System.currentTimeMillis();
    Path filename = Paths.get(args[0]);
    long crcValue = checksumInputStream(filename);
    long end = System.currentTimeMillis();
    System.out.println(Long.toHexString(crcValue));
    System.out.println((end - start) + " milliseconds");

    System.out.println("Buffered Input Stream:");
    start = System.currentTimeMillis();
    crcValue = checksumBufferedInputStream(filename);
    end = System.currentTimeMillis();
    System.out.println(Long.toHexString(crcValue));
    System.out.println((end - start) + " milliseconds");

    System.out.println("Random Access File:");
    start = System.currentTimeMillis();
    crcValue = checksumRandomAccessFile(filename);
    end = System.currentTimeMillis();
    System.out.println(Long.toHexString(crcValue));
    System.out.println((end - start) + " milliseconds");

    System.out.println("Mapped File:");
    start = System.currentTimeMillis();
    crcValue = checksumMappedFile(filename);
    end = System.currentTimeMillis();
    System.out.println(Long.toHexString(crcValue));
    System.out.println((end - start) + " milliseconds");
}
}
```

### java.io.FileInputStream 1.0

| 方法 | 版本 | 描述 |
|---|---|---|
| `FileChannel getChannel()` | 1.4 | returns a channel for accessing this input stream. |

### java.io.FileOutputStream 1.0

| 方法 | 版本 | 描述 |
|---|---|---|
| `FileChannel getChannel()` | 1.4 | returns a channel for accessing this output stream. |

### java.io.RandomAccessFile 1.0

| 方法 | 版本 | 描述 |
|---|---|---|
| `FileChannel getChannel()` | 1.4 | returns a channel for accessing this file. |

### java.nio.channels.FileChannel 1.4

- `static FileChannel open(Path path, OpenOption... options)` 7
  - opens a file channel for the given path. By default, the channel is opened for reading.
  - **Parameters:**
    - `path` The path to the file on which to open the channel
    - `options` Values `WRITE`, `APPEND`, `TRUNCATE_EXISTING`, `CREATE` in the `StandardOpenOption` enumeration
- `MappedByteBuffer map(FileChannel.MapMode mode, long position, long size)`
  - maps a region of the file to memory.
  - **Parameters:**
    - `mode` One of the constants `READ_ONLY`, `READ_WRITE`, or `PRIVATE` in the `FileChannel.MapMode` class
    - `position` The start of the mapped region
    - `size` The size of the mapped region

### java.nio.Buffer 1.4

- `boolean hasRemaining()`
  - returns true if the current buffer position has not yet reached the buffer's limit position.
- `int limit()`
  - returns the limit position of the buffer—that is, the first position at which no more values are available.

### java.nio.ByteBuffer 1.4

- `byte get()`
  - gets a byte from the current position and advances the current position to the next byte.
- `byte get(int index)`
  - gets a byte from the specified index.
- `ByteBuffer put(byte b)`
  - puts a byte at the current position and advances the current position to the next byte. Returns a reference to this buffer.
- `ByteBuffer put(int index, byte b)`
  - puts a byte at the specified index. Returns a reference to this buffer.
- `ByteBuffer get(byte[] destination)`
- `ByteBuffer get(byte[] destination, int offset, int length)`
  - fills a byte array, or a region of a byte array, with bytes from the buffer, and advances the current position by the number of bytes read. If not enough bytes remain in the buffer, then no bytes are read, and a `BufferUnderflowException` is thrown. Returns a reference to this buffer.

  **Parameters:**

  | Parameter | Description |
  | --- | --- |
  | `destination` | The byte array to be filled |
  | `offset` | The offset of the region to be filled |
  | `length` | The length of the region to be filled |

- `ByteBuffer put(byte[] source)`
- `ByteBuffer put(byte[] source, int offset, int length)`
  - puts all bytes from a byte array, or the bytes from a region of a byte array, into the buffer, and advances the current position by the number of bytes read. If not enough bytes remain in the buffer, then no bytes are written, and a `BufferOverflowException` is thrown. Returns a reference to this buffer.

  **Parameters:**

  | Parameter | Description |
  | --- | --- |
  | `source` | The byte array to be written |
  | `offset` | The offset of the region to be written |
  | `length` | The length of the region to be written |

- `Xxx getXxx()`
- `Xxx getXxx(int index)`
- `ByteBuffer putXxx(Xxx value)`
- `ByteBuffer putXxx(int index, Xxx value)`
  - gets or puts a binary number. `Xxx` is one of `Int`, `Long`, `Short`, `Char`, `Float`, or `Double`.
- `ByteBuffer order(ByteOrder order)`
- `ByteBuffer order()`
  - sets or gets the byte order. The value for `order` is one of the constants `BIG_ENDIAN` or `LITTLE_ENDIAN` of the `ByteOrder` class.
- `static ByteBuffer allocate(int capacity)`
  - constructs a buffer with the given capacity.
- `static ByteBuffer wrap(byte[] values)`
  - constructs a buffer that is backed by the given array.
- `CharBuffer asCharBuffer()`
  - constructs a character buffer that is backed by this buffer. Changes to the character buffer will show up in this buffer, but the character buffer has its own position, limit, and mark.

### java.nio.CharBuffer 1.4

| 方法 | 描述 |
|---|---|
| `char get()`<br>`CharBuffer get(char[] destination)`<br>`CharBuffer get(char[] destination, int offset, int length)` | gets one char value, or a range of char values, starting at the buffer's position and moving the position past the characters that were read. The last two methods return this. |
| `CharBuffer put(char c)`<br>`CharBuffer put(char[] source)`<br>`CharBuffer put(char[] source, int offset, int length)`<br>`CharBuffer put(String source)`<br>`CharBuffer put(CharBuffer source)` | puts one char value, or a range of char values, starting at the buffer's position and advancing the position past the characters that were written. When reading from a CharBuffer, all remaining characters are read. All methods return this. |

## 2.6.2 The Buffer Data Structure

When you use memory mapping, you make a single buffer that spans the entire file or the area of the file that you're interested in. You can also use buffers to read and write more modest chunks of information.

In this section, we briefly describe the basic operations on Buffer objects. A buffer is an array of values of the same type. The Buffer class is an abstract class with concrete subclasses ByteBuffer, CharBuffer, DoubleBuffer, FloatBuffer, IntBuffer, LongBuffer, and ShortBuffer.

> **NOTE:** The StringBuffer class is not related to these buffers.

In practice, you will most commonly use ByteBuffer and CharBuffer. As shown in Figure 2.10, a buffer has

- A *capacity* that never changes
- A *position* at which the next value is read or written
- A *limit* beyond which reading and writing is meaningless
- Optionally, a *mark* for repeating a read or write operation
