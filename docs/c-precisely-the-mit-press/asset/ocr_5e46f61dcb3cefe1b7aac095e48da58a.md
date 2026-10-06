# Example 190 Binary Input and Output of Simple Type Data

Method WriteData demonstrates writing simple data to a BinaryWriter, and method ReadData demonstrates all ways to read simple values from a BinaryReader. The methods complement each other, after writing a stream with WriteData, one can read ReadData. Namely, an integer written using BinaryWriter's method Write(Int) can be read using BinaryReader's method ReadInt32().

```
public static void main() {
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
    bw.Write((byte)(sbyte-1);
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
    Console.Write(" " + br.ReadUInt16(());
    Console.Write(" " + br.ReadUInt16());
    Console.WriteLine();
}
```

# Example 191 Binary Input/Output to Random Access File

See examples 192 and 193.