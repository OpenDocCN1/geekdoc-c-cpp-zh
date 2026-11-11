# Listing 2.5 *(Continued)*

```
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
```
```