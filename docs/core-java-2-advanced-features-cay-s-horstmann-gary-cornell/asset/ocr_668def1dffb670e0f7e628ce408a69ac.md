**java.io.FileOutputStream** 1.0

- `FileOutputStream(String name)`
- `FileOutputStream(String name, boolean append)`
- `FileOutputStream(File file)`
- `FileOutputStream(File file, boolean append)`

Creates a new file output stream specified by the name string or the file object. (The File class is described at the end of this chapter.) If the append parameter is true, an existing file with the same name will not be deleted and data will be added at the end of the file. Otherwise, this method deletes any existing file with the same name.

**java.io.BufferedInputStream** 1.0

- `BufferedInputStream(InputStream in)`

Creates a buffered input stream. A buffered input stream reads bytes from a stream without causing a device access every time. When the buffer is empty, a new block of data is read into the buffer.

**java.io.BufferedOutputStream** 1.0

- `BufferedOutputStream(OutputStream out)`

Creates a buffered output stream. A buffered output stream collects bytes to be written without causing a device access every time. When the buffer fills up or when the stream is flushed, the data are written.

**java.io.PushbackInputStream** 1.0

- `PushbackInputStream(InputStream in)`
- `PushbackInputStream(InputStream in, int size)`

Constructs an input stream with one-byte lookahead or a pushback buffer of specified size.

- `void unread(int b)`

Pushes back a byte, which is retrieved again by the next call to read.

*Parameters:* `b` — The byte to be read again