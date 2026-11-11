
![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_82_0.png)

**Figure 2.1** Input and output stream hierarchy

and

```java
void flush()
```

respectively. The classes InputStream, OutputStream, Reader, and Writer all implement the Closeable interface.

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_83_0.png)

Figure 2.2 Reader and writer hierarchy

> **NOTE:** The java.io.Closeable interface extends the java.lang.AutoCloseable interface. Therefore, you can use the try-with-resources statement with any Closeable. Why have two interfaces? The close method of the Closeable interface only throws an IOException, whereas the AutoCloseable.close method may throw any exception.

OutputStream and Writer implement the Flushable interface.

The Readable interface has a single method

```java
int read(CharBuffer cb)
```

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_84_0.png)

**Figure 2.3** The Closeable, Flushable, Readable, and Appendable interfaces

The CharBuffer class has methods for sequential and random read/write access. It represents an in-memory buffer or a memory-mapped file. (See Section 2.5.2, “The Buffer Data Structure,” on p. 132 for details.)

The Appendable interface has two methods for appending single characters and character sequences:

```java
Appendable append(char c)
Appendable append(CharSequence s)
```

The CharSequence interface describes basic properties of a sequence of char values. It is implemented by String, CharBuffer, StringBuilder, and StringBuffer.

Of the input/output stream classes, only Writer implements Appendable.

| `java.io.Closeable` | 5.0 |
|---|---|
| • `void close()` | closes this Closeable. This method may throw an IOException. |

| `java.io.Flushable` | 5.0 |
|---|---|
| • `void flush()` | flushes this Flushable. |

| `java.lang.Readable` | 5.0 |
|---|---|
| • `int read(CharBuffer cb)` | attempts to read as many char values into cb as it can hold. Returns the number of values read, or -1 if no further values are available from this Readable. |

| `java.lang.Appendable` | 5.0 |
|---|---|
| • `Appendable append(char c)`<br>• `Appendable append(CharSequence cs)` | appends the given code unit, or all code units in the given sequence, to this Appendable; returns this. |

| `java.lang.CharSequence` | 1.4 |
|---|---|
| • `char charAt(int index)` | returns the code unit at the given index. |
| • `int length()` | returns the number of code units in this sequence. |
| • `CharSequence subSequence(int startIndex, int endIndex)` | returns a CharSequence consisting of the code units stored from index startIndex to endIndex - 1. |
| • `String toString()` | returns a string consisting of the code units of this sequence. |

## 2.1.3 Combining Input/Output Stream Filters

FileInputStream and FileOutputStream give you input and output streams attached to a disk file. You need to pass the file name or full path name of the file to the constructor. For example,

```java
var fin = new FileInputStream("employee.dat");
```

looks in the user directory for a file named employee.dat.

> **TIP:** All the classes in java.io interpret relative path names as starting from the user's working directory. You can get this directory by a call to System.getProperty("user.dir").

> **CAUTION:** Since the backslash character is the escape character in Java strings, be sure to use `\\` for Windows-style path names (for example, `C:\\Windows\\win.ini`). In Windows, you can also use a single forward slash (`C:/Windows/win.ini`) because most Windows file-handling system calls will interpret forward slashes as file separators. However, this is not recommended—the behavior of the Windows system functions is subject to change. Instead, for portable programs, use the file separator character for the platform on which your program runs. It is available as the constant string `java.io.File.separator`.

Like the abstract InputStream and OutputStream classes, these classes only support reading and writing at the byte level. That is, we can only read bytes and byte arrays from the object fin.

```java
byte b = (byte) fin.read();
```

As you will see in the next section, if we just had a DataInputStream, we could read numeric types:

```java
DataInputStream din = ...;
double x = din.readDouble();
```

But just as the FileInputStream has no methods to read numeric types, the DataInputStream has no method to get data from a file.

Java uses a clever mechanism to separate two kinds of responsibilities. Some input streams (such as the FileInputStream and the input stream returned by the openStream method of the URL class) can retrieve bytes from files and other more exotic locations. Other input streams (such as the DataInputStream) can assemble bytes into more useful data types. The Java programmer has to combine the two. For example, to be able to read numbers from a file, first create a FileInputStream and then pass it on to the constructor of a DataInputStream.

```java
var fin = new FileInputStream("employee.dat");
var din = new DataInputStream(fin);
double x = din.readDouble();
```

If you look at Figure 2.1 again, you can see the classes FilterInputStream and FilterOutputStream. The subclasses of these classes are used to add capabilities to input/output streams that process bytes.

You can add multiple capabilities by nesting the filters. For example, by default, input streams are not buffered. That is, every call to read asks the operating system to dole out yet another byte. It is more efficient to request blocks of data instead and store them in a buffer. If you want buffering *and* the data input methods for a file, use the following rather monstrous sequence of constructors:

```java
var din = new DataInputStream(
    new BufferedInputStream(
        new FileInputStream("employee.dat")));
```

Notice that we put the DataInputStream *last* in the chain of constructors because we want to use the DataInputStream methods, and we want *them* to use the buffered read method.

Sometimes you'll need to keep track of the intermediate input streams when chaining them together. For example, when reading input, you often need to peek at the next byte to see if it is the value that you expect. Java provides the PushbackInputStream for this purpose.

```java
var pbin = new PushbackInputStream(
    new BufferedInputStream(
        new FileInputStream("employee.dat")));
```

Now you can speculatively read the next byte

```java
int b = pbin.read();
```

and throw it back if it isn't what you wanted.

```java
if (b != '<') pbin.unread(b);
```

However, reading and unreading are the *only* methods that apply to a pushback input stream. If you want to look ahead and also read numbers, then you need both a pushback input stream and a data input stream reference.

```java
var pbin = new PushbackInputStream(
    new BufferedInputStream(
        new FileInputStream("employee.dat")));
var din = new DataInputStream(pbin);
```

Of course, in the input/output libraries of other programming languages, niceties such as buffering and lookahead are automatically taken care of—so it is a bit of a hassle to resort, in Java, to combining stream filters. However, the ability to mix and match filter classes to construct useful sequences of

### java.io.FileOutputStream 1.0

- `FileOutputStream(String name)`
- `FileOutputStream(String name, boolean append)`
- `FileOutputStream(File file)`
- `FileOutputStream(File file, boolean append)`

creates a new file output stream specified by the name string or the file object. (The `File` class is described at the end of this chapter.) If the `append` parameter is true, an existing file with the same name will not be deleted and data will be added at the end of the file. Otherwise, this method deletes any existing file with the same name.

### java.io.BufferedInputStream 1.0

- `BufferedInputStream(InputStream in)`

creates a buffered input stream. A buffered input stream reads bytes from a stream without causing a device access every time. When the buffer is empty, a new block of data is read into the buffer.

### java.io.BufferedOutputStream 1.0

- `BufferedOutputStream(OutputStream out)`

creates a buffered output stream. A buffered output stream collects bytes to be written without causing a device access every time. When the buffer fills up or when the stream is flushed, the data are written.

### java.io.PushbackInputStream 1.0

- `PushbackInputStream(InputStream in)`
- `PushbackInputStream(InputStream in, int size)`

constructs an input stream with one-byte lookahead or a pushback buffer of specified size.

- `void unread(int b)`

pushes back a byte, which is retrieved again by the next call to `read`.
