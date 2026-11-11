![](bbox=[0.227, 0.16, 0.86, 0.491])

**Figure 2.3** The Closeable, Flushable, Readable, and Appendable interfaces

The Appendable interface has two methods for appending single characters and character sequences:

```
Appendable append(char c)
Appendable append(CharSequence s)
```

The CharSequence interface describes basic properties of a sequence of char values. It is implemented by String, CharBuffer, StringBuilder, and StringBuffer.

Of the input/output stream classes, only Writer implements Appendable.

| java.io.Closeable 5.0 |
|---|
| • `void close()`<br>closes this Closeable. This method may throw an IOException. |