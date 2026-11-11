
`get(byte[] bytes)` 和 `get(byte[], int offset, int length)`

最后，还有 `getInt`、`getLong`、`getShort`、`getChar`、`getFloat`、`getDouble` 等方法，用于读取以 *二进制* 值形式存储在文件中的基本类型值。正如我们已经提到的，Java 对二进制数据使用大端序。但是，如果你需要处理包含小端序二进制数的文件，只需调用

`buffer.order(ByteOrder.LITTLE_ENDIAN);`

要查明缓冲区的当前字节顺序，请调用

`ByteOrder b = buffer.order();`

> **警告：** 这对方法不使用 set/get 命名约定。

要将数字写入缓冲区，请使用 `putInt`、`putLong`、`putShort`、`putChar`、`putFloat`、`putDouble` 等方法之一。

在某个时刻，尤其是在通道关闭时，这些更改会被写回文件。

清单 2.5 计算文件的 32 位循环冗余校验（CRC32）。该校验和常用于判断文件是否已损坏。文件损坏很可能使校验和发生变化。`java.util.zip` 包包含一个 `CRC32` 类，它使用以下循环计算字节序列的校验和：

```java
CRC32 crc = new CRC32();
while (more bytes)
    crc.update(next byte)
long checksum = crc.getValue();
```

## 清单 2.5 *(续)*

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
| `FileChannel getChannel()` | 1.4 | 返回用于访问此输入流的通道。 |

### java.io.FileOutputStream 1.0

| 方法 | 版本 | 描述 |
|---|---|---|
| `FileChannel getChannel()` | 1.4 | 返回用于访问此输出流的通道。 |

### java.io.RandomAccessFile 1.0

| 方法 | 版本 | 描述 |
|---|---|---|
| `FileChannel getChannel()` | 1.4 | 返回用于访问此文件的通道。 |

### java.nio.channels.FileChannel 1.4

- `static FileChannel open(Path path, OpenOption... options)` 7
  - 为给定路径打开文件通道。默认情况下，该通道以读取方式打开。
  - **参数：**
    - `path` 要在其上打开通道的文件路径
    - `options` `StandardOpenOption` 枚举中的值 `WRITE`、`APPEND`、`TRUNCATE_EXISTING`、`CREATE`
- `MappedByteBuffer map(FileChannel.MapMode mode, long position, long size)`
  - 将文件的一个区域映射到内存。
  - **参数：**
    - `mode` `FileChannel.MapMode` 类中的常量 `READ_ONLY`、`READ_WRITE` 或 `PRIVATE` 之一
    - `position` 映射区域的起始位置
    - `size` 映射区域的大小

### java.nio.Buffer 1.4

- `boolean hasRemaining()`
  - 如果当前缓冲区位置尚未到达缓冲区的限制位置，则返回 true。
- `int limit()`
  - 返回缓冲区的限制位置——即不再有可用值的第一个位置。

### java.nio.ByteBuffer 1.4

- `byte get()`
  - 从当前位置获取一个字节，并将当前位置推进到下一个字节。
- `byte get(int index)`
  - 从指定索引处获取一个字节。
- `ByteBuffer put(byte b)`
  - 在当前位�置放入一个字节，并将当前位置推进到下一个字节。返回对此缓冲区的引用。
- `ByteBuffer put(int index, byte b)`
  - 在指定索引处放入一个字节。返回对此缓冲区的引用。
- `ByteBuffer get(byte[] destination)`
- `ByteBuffer get(byte[] destination, int offset, int length)`
  - 用缓冲区中的字节填充一个字节数组或字节数组的某个区域，并将当前位置推进读取的字节数。如果缓冲区中剩余字节不足，则不读取任何字节，并抛出 `BufferUnderflowException`。返回对此缓冲区的引用。

  **参数：**

  | 参数 | 描述 |
  | --- | --- |
  | `destination` | 要填充的字节数组 |
  | `offset` | 要填充区域的偏移量 |
  | `length` | 要填充区域的长度 |

- `ByteBuffer put(byte[] source)`
- `ByteBuffer put(byte[] source, int offset, int length)`
  - 将一个字节数组中的所有字节或字节数组中某个区域的字节放入缓冲区，并将当前位置推进相应字节数。如果缓冲区中剩余字节不足，则不写入任何字节，并抛出 `BufferOverflowException`。返回对此缓冲区的引用。

  **参数：**

  | 参数 | 描述 |
  | --- | --- |
  | `source` | 要写入的字节数组 |
  | `offset` | 要写入区域的偏移量 |
  | `length` | 要写入区域的长度 |

- `Xxx getXxx()`
- `Xxx getXxx(int index)`
- `ByteBuffer putXxx(Xxx value)`
- `ByteBuffer putXxx(int index, Xxx value)`
  - 获取或放入一个二进制数。`Xxx` 是 `Int`、`Long`、`Short`、`Char`、`Float` 或 `Double` 之一。
- `ByteBuffer order(ByteOrder order)`
- `ByteBuffer order()`
  - 设置或获取字节顺序。`order` 的值为 `ByteOrder` 类的常量 `BIG_ENDIAN` 或 `LITTLE_ENDIAN` 之一。
- `static ByteBuffer allocate(int capacity)`
  - 构造一个具有给定容量的缓冲区。
- `static ByteBuffer wrap(byte[] values)`
  - 构造一个由给定数组支持的缓冲区。
- `CharBuffer asCharBuffer()`
  - 构造一个由此缓冲区支持的字符缓冲区。对字符缓冲区的更改将反映在此缓冲区中，但字符缓冲区有其自己的位置、限制和标记。

### java.nio.CharBuffer 1.4

| 方法 | 描述 |
|---|---|
| `char get()`<br>`CharBuffer get(char[] destination)`<br>`CharBuffer get(char[] destination, int offset, int length)` | 从缓冲区的位置开始获取一个 char 值或一段 char 值，并将位置移过已读取的字符。后两个方法返回 this。 |
| `CharBuffer put(char c)`<br>`CharBuffer put(char[] source)`<br>`CharBuffer put(char[] source, int offset, int length)`<br>`CharBuffer put(String source)`<br>`CharBuffer put(CharBuffer source)` | 从缓冲区的位置开始放入一个 char 值或一段 char 值，并将位置推进到已写入字符之后。从 CharBuffer 读取时，会读取所有剩余字符。所有方法都返回 this。 |

## 2.6.2 缓冲区数据结构

使用内存映射时，你会创建一个跨越整个文件或文件中你感兴趣区域的单一缓冲区。你也可以使用缓冲区来读写更小数据块的信息。

本节简要描述 Buffer 对象的基本操作。缓冲区是同一类型值的数组。Buffer 类是一个抽象类，具体子类有 ByteBuffer、CharBuffer、DoubleBuffer、FloatBuffer、IntBuffer、LongBuffer 和 ShortBuffer。

> **注意：** StringBuffer 类与这些缓冲区无关。

在实践中，你最常使用的是 ByteBuffer 和 CharBuffer。如图 2.10 所示，缓冲区具有

- 一个永不改变的*容量*
- 一个*位置*，在此读取或写入下一个值
- 一个*限制*，超过该限制的读写没有意义
- 可选的*标记*，用于重复读或写操作

