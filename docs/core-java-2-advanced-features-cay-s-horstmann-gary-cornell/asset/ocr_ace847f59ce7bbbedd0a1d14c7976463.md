# java.nio.channels.FileChannel 1.4

+   * static FileChannel open(Path path, OpenOption... options) 7
+     opens a file channel for the given path. By default, the channel is opened for reading.
+     *Parameters:*
+       path The path to the file on which to open the channel
+       options Values WRITE, APPEND,TRUNCATE_EXISTING, CREATE in the StandardOpenOption enumeration

+   * MappedByteBuffer map(FileChannel.MapMode mode, long position, long size)
+     maps a region of the file to memory.
+     *Parameters:*
+       mode One of the constants READ_ONLY, READ_WRITE, or PRIVATE in the FileChannel.MapMode class
+       position The start of the mapped region
+       size The size of the mapped region

# java.nio.Buffer 1.4

+   * boolean hasRemaining()
+     returns true if the current buffer position has not yet reached the buffer's limit position.

+   * int limit()
+     returns the limit position of the buffer—that is, the first position at which no more values are available.

# java.nio.ByteBuffer 1.4

+   * byte get()
+     gets a byte from the current position and advances the current position to the next byte.

+   * byte get(int index)
+     gets a byte from the specified index.

+   * ByteBuffer put(byte b)
+     puts a byte at the current position and advances the current position to the next byte. Returns a reference to this buffer.

+   * ByteBuffer put(int index, byte b)
+     puts a byte at the specified index. Returns a reference to this buffer.