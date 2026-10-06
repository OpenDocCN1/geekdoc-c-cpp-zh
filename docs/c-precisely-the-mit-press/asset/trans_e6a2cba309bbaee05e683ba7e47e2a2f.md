

# 示例 190 简单类型数据的二进制输入输出

`WriteData` 方法演示了如何向 `BinaryWriter` 写入简单数据，`ReadData` 方法演示了从 `BinaryReader` 读取简单值的所有方法。这些方法互为补充：在用 `WriteData` 写入流后，可以使用 `ReadData` 进行读取。例如，使用 `BinaryWriter` 的 `Write(Int)` 方法写入的整数可以使用 `BinaryReader` 的 `ReadInt32()` 方法读取。

```cpublic static void main() {
    BinaryWriter bw = new BinaryWriter(new FileStream("tmpl.dat", FileMode.Create));
    WriteData(bw); bw.Close();
    BinaryReader br = new BinaryReader(new FileStream("tmpl.dat", FileMode.Open));
    ReadData(br);
}

static void WriteData(BinaryWriter bw) {
    bw.Write(true);
    bw.Write((byte)120);
    bw.Write('A');
    bw.Write("fogg");
    bw.Write("Random");
    bw.Write(300.1);
    bw.Write(300.2F);
    bw.Write(1234);
    bw.Write(12345L);
    bw.Write((short)32000);
    bw.Write((byte)(sbyte-1));
    bw.Write((short)-1);
}

static void ReadData(BinaryReader br) {
    Console.Write(" " + br.ReadBoolean());
    Console.Write(" " + br.ReadByte());
    Console.Write(" " + br.ReadChar());
    Console.Write(" " + br.ReadString());
    Console.Write(" " + br.ReadInt16());
    Console.Write(" " + br.ReadDouble());
    Console.Write(" " + br.ReadSingle());
    Console.Write(" " + br.ReadInt32());
    Console.Write(" " + br.ReadInt64());
    Console.Write(" " + br.ReadInt16());
    Console.Write(" " + br.ReadByte());
    Console.Write(" " + br.ReadUInt16());
    Console.Write(" " + br.ReadUInt16());
    Console.WriteLine();
}
```

# 示例 191 随机访问文件的二进制输入/输出

参见示例 192 和 193。

## 25.7 字节输入与输出：流

抽象类 `Stream` 及其子类（所有名称都以 `Stream` 结尾）用于面向字节的输入和输出。流与某些资源关联，以便读取或写入，通常是文件或内存区域。流可能支持读取、寻求、写入或这些者的组合。流有一个当前位置，指示要从哪个字节读取或写入。假设 `s` 是一个 `Stream` 类型的变量：

- 只读属性 `s.CanRead`：如果流未关闭且支持读取，则为 `true`；否则为 `false`。
- 只读属性 `s.CanSeek`：如果流未关闭且支持寻求，则为 `true`；否则为 `false`。
- 只读属性 `s.CanWrite`：如果流未关闭且支持写入，则为 `true`；否则为 `false`。
- 类型为 `long` 的只读属性 `s.Length`：是流中的字节数，如果流支持寻求；否则抛出 `UnsupportedException`。
- 类型为 `long` 的读写属性 `s.Position`：返回流的当前位置。将 `s.Position` 设置为 `v` 可将流的当前位置设置为 `v`。

`Stream` 类（以及任何子类型）变量具有以下方法：

- `int ReadByte()`：读取一个（0...255）并作为 `int` 返回，阻塞直到输入可用；在流末尾时返回 `-1`。
- `int Read(byte[] b, int i, int n)`：从流中读取最多 `n` 个字节并复制到 `b[i..i+n-1]` 中，返回字节数。
- `void Seek(long v, SeekOrigin origin)`：将流的位置移动到指定位置。
- `void SetLength(long v)`：设置流的长度。
- `void Write(byte v)`：向流写入一个字节。
- `void Write(byte[] b, int i, int n)`：向流写入 `b` 中从 `i` 开始的 `n` 个字节。
- `void Write(string v)`：向流写入一个字符串。
- `void Write(int v)`：向流写入一个整数。
- `void Write(short v)`：向流写入一个短整数。
- `void Write(long v)`：向流写入一个长整数。
- `void Write(float v)`：向流写入一个单精度浮点数。
- `void Write(double v)`：向流写入一个双精度浮点数。
- `void Flush()`：将缓冲区的数据写入底层流。
- `void Close()`：关闭流并释放资源。

# 示例 192 为随机访问组织字符串数组

此示例展示了如何实现大量的文本、缓存页面或 DNA 序列。定义字符串数组包含三部分：(1) 字符串序列，格式为 UTF-8；(2) 整数序列，表示字符串的偏移量；(3) 一个整数，表示文件中的字符串数量。

将字符串数量和字符串偏移放在文件的末尾，这样在写入文件之前不需要知道字符串的数量或每个字符串的长度。字符串可以增量地写入文件，内存中唯一需要的结构是字符串表。该表表示为 `List<Long>` 以确保类型安全和性能。

```cs
static void WriteStrings(String filename, String[] data) {
    FileStream raf = new FileStream(filename, FileMode.Create);
    BinaryWriter sw = new BinaryWriter(raf);
    raf.SetLength(0); // 截断文件
    List<Long> offset = new List<Long>();
    foreach (string s in data) {
        offset.Add(raf.Position);
        sw.Write(s);
    }
    sw.Write(data.Count);
    foreach (long o in offset) {
        sw.Write(o);
    }
    sw.Close();
    raf.Close();
}
```

# 示例 193 随机访问文件字符串

此示例演示了如何根据偏移表通过随机访问从文件中读取字符串。

```cs
static string[] ReadStrings(String filename) {
    FileStream raf = new FileStream(filename, FileMode.Open);
    BinaryReader br = new BinaryReader(raf);
    int count = br.ReadInt32();
    long[] offset = new long[count];
    for (int i = 0; i < count; i++) {
        offset[i] = br.ReadInt64();
    }
    string[] data = new string[count];
    for (int i = 0; i < count; i++) {
        raf.Seek(offset[i], SeekOrigin.Begin);
        data[i] = br.ReadString();
    }
    br.Close();
    raf.Close();
    return data;
}
```

