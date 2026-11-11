
## 代码清单 2.5（续）

```java
public class MemoryMapTest
{
    public static long checksumInputStream(Path filename) throws IOException
    {
        try (InputStream in = Files.newInputStream(filename))
        {
            var crc = new CRC32();

            int c;
            while ((c = in.read()) != -1)
                crc.update(c);
            return crc.getValue();
        }
    }

    public static long checksumBufferedInputStream(Path filename) throws IOException
    {
        try (var in = new BufferedInputStream(Files.newInputStream(filename)))
        {
            var crc = new CRC32();

            int c;
            while ((c = in.read()) != -1)
                crc.update(c);
            return crc.getValue();
        }
    }

    public static long checksumRandomAccessFile(Path filename) throws IOException
    {
        try (var file = new RandomAccessFile(filename.toFile(), "r"))
        {
            long length = file.length();
            var crc = new CRC32();

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
            var crc = new CRC32();
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

### java.nio.ByteBuffer 1.4

- `byte get()`  
  从当前位置获取一个字节，并将当前位置推进到下一个字节。
- `byte get(int index)`  
  从指定索引处获取一个字节。
- `ByteBuffer put(byte b)`  
  在当前���置放入一个字节，并将当前位置推进到下一个字节。返回对该缓冲区的引用。
- `ByteBuffer put(int index, byte b)`  
  在指定索引处放入一个字节。返回对该缓冲区的引用。
- `ByteBuffer get(byte[] destination)`  
- `ByteBuffer get(byte[] destination, int offset, int length)`  
  用缓冲区中的字节填充一个字节数组或字节数组的某个区域，并将当前位置前进读取的字节数。如果缓冲区中剩余字节不足，则不读取任何字节，并抛出 `BufferUnderflowException`。返回对该缓冲区的引用。
- `ByteBuffer put(byte[] source)`  
- `ByteBuffer put(byte[] source, int offset, int length)`  
  将字节数组中的所有字节，或字节数组某个区域中的字节，放入缓冲区，并将当前位置前进读取的字节数。如果缓冲区中剩余字节不足，则不写入任何字节，并抛出 `BufferOverflowException`。返回对该缓冲区的引用。
- `Xxx getXxx()`  
- `Xxx getXxx(int index)`  
- `ByteBuffer putXxx(Xxx value)`  
- `ByteBuffer putXxx(int index, Xxx value)`  
  获取或放入一个二进制数。`Xxx` 是 `Int`、`Long`、`Short`、`Char`、`Float` 或 `Double` 之一。
- `ByteBuffer order(ByteOrder order)`  
- `ByteOrder order()`  
  设置或获取字节顺序。order 的值为 `ByteOrder` 类的常量 `BIG_ENDIAN` 或 `LITTLE_ENDIAN` 之一。
- `static ByteBuffer allocate(int capacity)`  
  构造一个具有给定容量的缓冲区。

### java.nio.ByteBuffer 1.4 *（续）*

| 方法 | 描述 |
|---|---|
| `static ByteBuffer wrap(byte[] values)` | 构造一个由给定数组支持的缓冲区。 |
| `CharBuffer asCharBuffer()` | 构造一个由此缓冲区支持的字符缓冲区。对字符缓冲区的更改会反映到此缓冲区中，但字符缓冲区有自己的位置、限制和标记。 |

### java.nio.CharBuffer 1.4

| 方法 | 描述 |
|---|---|
| `char get()`<br>`CharBuffer get(char[] destination)`<br>`CharBuffer get(char[] destination, int offset, int length)` | 从缓冲区的位置开始获取一个 char 值或一段 char 值，并将位置移过已读取的字符。最后两个方法返回 this。 |
| `CharBuffer put(char c)`<br>`CharBuffer put(char[] source)`<br>`CharBuffer put(char[] source, int offset, int length)`<br>`CharBuffer put(String source)`<br>`CharBuffer put(CharBuffer source)` | 从缓冲区的位置开始放入一个 char 值或一段 char 值，并将位置推进到已写入字符之后。从 CharBuffer 读取时，会读取所有剩余字符。所有方法均返回 this。 |

## 2.5.2 缓冲区数据结构

使用内存映射时，你会创建一个跨越整个文件或你所关心的文件区域的单一缓冲区。你也可以使用缓冲区来读写更小块的信息。

本节简要描述 Buffer 对象的基本操作。缓冲区是一个由相同类型的值组成的数组。Buffer 类是一个抽象类，具体子类包括 ByteBuffer、CharBuffer、DoubleBuffer、FloatBuffer、IntBuffer、LongBuffer 和 ShortBuffer。

> 注意：StringBuffer 类与这些缓冲区无关。

在实践中，你最常使用的是 `ByteBuffer` 和 `CharBuffer`。如图 2.9 所示，缓冲区具有

- *容量*，永不改变
- *位置*，即读取或写入下一个值的位置
- *限制*，超过该限制后读写便没有意义
- 可选地，*标记*，用于重复读或写操作

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_155_0.png)

**图 2.9** 缓冲区

这些值满足条件

$0 \leq mark \leq position \leq limit \leq capacity$

缓冲区的主要用途是“先写入，再读取”的循环。一开始，缓冲区的位置为 0，限制为容量。持续调用 put 向缓冲区添加值。当数据用完或达到容量时，就该切换到读取。

调用 flip 将限制设置为当前位置，并将位置设置为 0。现在，只要 remaining 方法（返回 *limit − position*）为正，就持续调用 get。读完缓冲区中的所有值后，调用 clear 为下一个写入循环做好准备。clear 方法将位置重置为 0，并将限制重置为容量。

如果要重新读取缓冲区，请使用 rewind 或 mark/reset（详情见 API 注释）。

要获得缓冲区，请调用静态方法，例如 `ByteBuffer.allocate` 或 `ByteBuffer.wrap`。然后，你可以从通道填充缓冲区，或将其内容写入通道。例如，
