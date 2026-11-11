| `java.nio.CharBuffer` | 1.4 |
|---|---|
| • `char get()`<br>• `CharBuffer get(char[] destination)`<br>• `CharBuffer get(char[] destination, int offset, int length)` | gets one char value, or a range of char values, starting at the buffer’s position and moving the position past the characters that were read. The last two methods return this. |
| • `CharBuffer put(char c)`<br>• `CharBuffer put(char[] source)`<br>• `CharBuffer put(char[] source, int offset, int length)`<br>• `CharBuffer put(String source)`<br>• `CharBuffer put(CharBuffer source)` | puts one char value, or a range of char values, starting at the buffer’s position and advancing the position past the characters that were written. When reading from a CharBuffer, all remaining characters are read. All methods return this. |

# 2.6.2  The Buffer Data Structure

When you use memory mapping, you make a single buffer that spans the entire file or the area of the file that you’re interested in. You can also use buffers to read and write more modest chunks of information.

In this section, we briefly describe the basic operations on Buffer objects. A buffer is an array of values of the same type. The Buffer class is an abstract class with concrete subclasses ByteBuffer, CharBuffer, DoubleBuffer, FloatBuffer, IntBuffer, LongBuffer, and ShortBuffer.

> **NOTE:** The StringBuffer class is not related to these buffers.

In practice, you will most commonly use ByteBuffer and CharBuffer. As shown in Figure 2.10, a buffer has

+   - A *capacity* that never changes
+   - A *position* at which the next value is read or written
+   - A *limit* beyond which reading and writing is meaningless
+   - Optionally, a *mark* for repeating a read or write operation