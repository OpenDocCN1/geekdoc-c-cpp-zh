```
```java
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
```
```