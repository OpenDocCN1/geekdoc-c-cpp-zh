# StreamWriting for Old Walter 449

```
try {
  // Allocate the resource and use it here.
} finally {
  // Close and dispose of the resource here.
}
```

After using the block, the StreamWriter no longer exists, and the fs variable still exists, assuming that you created the stream outside the using statement, rather than on the fly like this:

```
using(StreamWriter sw = new StreamWriter(new FileStream(...)))
```

Flushing and closing the writer has flushed and closed the stream as. If you try to carry out operations on the stream, you get an exception telling that you cannot access a closed object. Notice in the FileWrite using block to ensure I don't want to use fs. After that, the FileStream is handed off to the garbage collector.

Of course, the file you write to disks. Create and open a new file stream to the if you need to manage it with again.

Specifically, is aimed at manage cleaning of objects that implement the IDisposable interface (see Book II for interfaces). The using statement ensures that the object's Dispose() method gets called. Classes that implement IDisposable guarantee that they use a Dispose()—IDisposable is mainly about disposing resources, namely stuff in the outside world of the operating system, file handles and graphics resources. File opens a file handle that must be released, which is why I mention IDisposable here. (Many classes and structs implement IDisposable; your classes can, if necessary.)

I don't go IDisposable in this book, but you should plan to become familiar with it your C# powers. Implementing it correctly has to do the kind of indeterminate garbage disposal I mention briefly in Book II and can be complex. So using is for use with classes and structs that implement IDisposable, something that you can check in Help. It won't help you with just any kind of object. Note: The intrinsic C# types—int, double, char,do not implement Disposable. Class TextWriter, the base class for StreamWriter, does implement the interface. In help, that looks like this:

```
public abstract class StreamWriter : MarshalByRefObject, IDisposable
```

When in doubt, check Help if the classes or structs you plan to implement IDisposable.

![](bbox=[0.115, 0.258, 0.198, 0.323])

![](bbox=[0.115, 0.547, 0.198, 0.613])

Book III
Chapter 3
FileStream
Fishing