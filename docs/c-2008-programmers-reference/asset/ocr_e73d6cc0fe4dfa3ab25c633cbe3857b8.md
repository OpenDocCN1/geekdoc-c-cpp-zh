![](bbox=[0.17, 0.1, 0.83, 0.42])

Figure 11-8

# Compressions for Stream Objects

The System.IO.Compression namespace contains classes that provide basic compression and decompression services for streams. This namespace contains two classes for data compression: DeflateStream and GZipStream. Both support lossless compression and decompression and are designed for dealing with streams.

Compression is useful for reducing the size of data. If you have huge amount of data to store in your SQL database, for instance, you can save on disk space if you compress the data before saving it into a table. Moreover, because you are now saving smaller blocks of data into your database, the time spent in performing disk I/O is significantly reduced. The downside of compression is that it takes additional processing power from your machine (and requires additional processing time), and you need to factor in this additional time before deciding you want to use compression in your application.

Compression is extremely useful in cases where you need to transmit data over networks, especially slow and costly networks such as General Packet Radio Service (GPRS) connections. In such cases, using compression can drastically cut down the data size and reduce the overall cost of communication. Web Services are another area where using compression can provide a great advantage because XML data can be highly compressed.

But once you've decided the performance cost is worth it, you'll need help deciphering the utilization of these two compression classes, which is what this section is about.

# Compression

The compression classes read data (to be compressed) from a byte array, compress it, and store the results in a Stream object. For decompression, the compressed data stored in a Stream object is decompressed and then stored in another Stream object.

Let's see how you can perform compression. First, define the Compress() function, which takes in two parameters: algo and data. The first parameter specifies which algorithm to use (GZip or Deflate),