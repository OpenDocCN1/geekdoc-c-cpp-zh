# Part I: C# Fundamentals

To use the two helper functions, make the following changes to the statements:

```
static void Main(string[] args)
{
    byte[] compressedData = Compress("Gzip",
        System.Text.Encoding.ASCII.GetBytes(
        "This is a uncompressed string"));

    string compressedDataStr = byteArrayToString(compressedData);
    Console.WriteLine("Compressed: {0}", compressedDataStr);

    byte[] data = stringToByteArray(compressedDataStr);
    Console.WriteLine("Uncompressed: {0}",
        ASCIIEncoding.ASCII.GetString(Decompress("Gzip", data)));

    Console.ReadLine();
}
```

Figure 11-10 shows the output when using the two helper functions.

![](bbox=[0.22, 0.57, 0.72, 0.7])

Figure 11-10

Alternatively, you can also convert the compressed data to a Base64-encoded string, like this:

```
byte[] compressedData = Compress("Gzip",
    System.Text.Encoding.ASCII.GetBytes(
    "This is a uncompressed string"));

string compressedDataStr = Convert.ToBase64String(compressedData);
Console.WriteLine("Compressed: {0}", compressedDataStr);

byte[] data = Convert.FromBase64String(compressedDataStr);
Console.WriteLine("Uncompressed: {0}",
    ASCIIEncoding.ASCII.GetString(Decompress("Gzip", data)));
```

Figure 11-11 shows the output using the base64 encoding.

![](bbox=[0.22, 0.96, 0.72, 0.99])

Figure 11-11