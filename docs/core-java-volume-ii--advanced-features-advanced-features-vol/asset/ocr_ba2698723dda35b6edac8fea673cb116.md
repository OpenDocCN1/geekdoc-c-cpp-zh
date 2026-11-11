Instead of working with bytes, you can use one of many input/output classes that build upon the basic `InputStream` and `OutputStream` classes.

### `java.io.InputStream` 1.0

- `abstract int read()`  
  reads a byte of data and returns the byte read; returns -1 at the end of the input stream.

- `int read(byte[] b)`  
  reads into an array of bytes and returns the actual number of bytes read, or -1 at the end of the input stream; this method reads at most `b.length` bytes.

- `int read(byte[] b, int off, int len)`  
- `int readNBytes(byte[] b, int off, int len)`  
  reads up to `len` bytes, if available without blocking (read), or blocking until all values have been read (`readNBytes`). Values are placed into `b`, starting at `off`. Returns the actual number of bytes read, or -1 at the end of the input stream.

- `byte[] readAllBytes()`  
  yields an array of all bytes that can be read from this stream.

- `long transferTo(OutputStream out)`  
  transfers all bytes from this input stream to the given output stream, returning the number of bytes transferred. Neither stream is closed.

- `long skip(long n)`  
  skips `n` bytes in the input stream, returns the actual number of bytes skipped (which may be less than `n` if the end of the input stream was encountered).

- `int available()`  
  returns the number of bytes available, without blocking (recall that blocking means that the current thread loses its turn).

- `void close()`  
  closes the input stream.

- `void mark(int readlimit)`  
  puts a marker at the current position in the input stream (not all streams support this feature). If more than `readlimit` bytes have been read from the input stream, the stream is allowed to forget the marker.

- `void reset()`  
  returns to the last marker. Subsequent calls to read reread the bytes. If there is no current marker, the input stream is not reset.

- `boolean markSupported()`  
  returns true if the input stream supports marking.