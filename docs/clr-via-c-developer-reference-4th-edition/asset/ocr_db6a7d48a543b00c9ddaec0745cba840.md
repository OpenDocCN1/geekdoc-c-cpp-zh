# An Interesting IO.FileStream type

The System.FileStream type allows the user to open a file for reading and writing. To improve performance, the type's implementation makes use of a memory buffer. Only when the buffer fills does the flush the contents of the buffer to the file. A FileStream supports writing of bytes only. If you want to write characters and strings, you can use a System.IO.StreamWriter, as demonstrated in the following code.

```
FileStream fs = new FileStream("Data.dat", FileMode.Create);
StreamWriter sw = new StreamWriter(fs);
sw.Write("Hi there");
```

```
// The following call to Dispose is what you should do.
sw.Dispose();
// NOTE: StreamWriter.Dispose closes the FileStream;
// The FileStream doesn't have to be explicitly closed.
```

Notice that the StreamWriter's constructor takes a reference to a Stream object as a parameter, allowing reference to a FileStream object to be passed as an argument. Internally, the StreamWriter object saves the Stream's reference. When you write to a StreamWriter object, it buffers the data in its own memory buffer. When the buffer is full, the StreamWriter writes the data to the Stream.

When you're finished writing data via the StreamWriter, you should call Dispose. (Because the StreamWriter type implements the IDisposable interface, you can also use it with C# using statement.) This causes the StreamWriter object to flush its data to the Stream object and close the Stream object.

> Note You don't have to explicitly call Dispose on the FileStream object because the StreamWriter calls it for you. However, if you do Dispose explicitly, the FileStream will see that the object has already been cleaned up—the method does nothing and returns.

What do you think would happen if there were no code to explicitly call Dispose? Well, at some point, the garbage collector would correctly detect that the objects were garbage and finalize them. The garbage collector doesn't guarantee the order in which objects are finalized. If the FileStream object was finalized first, it would close the file. Then when the StreamWriter object was finalized, it would attempt to write data to the closed file, throwing an exception. If, on the other hand, the StreamWriter object was finalized first, the data would be safely written to the file.

7 You can override this behavior by calling StreamWriter's constructor that accepts a Boolean leaveOpen parameter.

CHAPTER 21 The Managed Heap and Garbage Collection 537