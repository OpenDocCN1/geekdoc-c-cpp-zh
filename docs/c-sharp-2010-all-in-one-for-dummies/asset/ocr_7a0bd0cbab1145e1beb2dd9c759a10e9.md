![](bbox=[0.04, 0.13, 0.17, 0.26])

It's a good practice to wrap most work with streams in using statements. Wrapping the StreamWriter or StreamReader in a using statement, for example, has the same effect as putting the use of the writer or reader in a try/finally exception-handling block. (See Book I for exceptions.) In fact, the compiler translates the using block into the same code it uses for a try/finally, which guarantees that the resources get cleaned up:

```
try
{
    // Allocate the resource and use it here.
}
finally
{
    // Close and dispose of the resource here.
}
```

![](bbox=[0.04, 0.46, 0.17, 0.59])

After the using block, the StreamWriter no longer exists, and the FileStream object can no longer be accessed. The fs variable still exists, assuming that you created the stream outside the using statement, rather than on the fly like this:

```
using(StreamWriter sw = new StreamWriter(new FileStream(...)) ...
```

Flushing and closing the writer has flushed and closed the stream as well. If you try to carry out operations on the stream, you get an exception telling you that you can't access a closed object. Notice that in the FileWrite code earlier in this section I nulled the FileStream object, fs, after the using block to ensure that I won't try to use fs again. After that, the FileStream object is handed off to the garbage collector.

Of course, the file you wrote to disk exists. Create and open a new file stream to the file if you need to work with it again.

![](bbox=[0.04, 0.8, 0.18, 0.92])

Specifically, using is aimed at managing cleanup of objects that implement the IDisposable interface (see Book II for information on interfaces). The using statement ensures that the object's Dispose() method gets called. Classes that implement IDisposable guarantee that they have a Dispose() method. IDisposable is mainly about disposing non-.NET resources, mainly stuff in the outside world of the Windows operating system, such as file handles and graphics resources. FileStream, for example, wraps a Windows file handle that must be released, which is why I mention IDisposable here. (Many classes and structs implement IDisposable; your classes can too, if necessary.)

I don't go into IDisposable in this book, but you should plan to become more familiar with it as your C# powers grow. Implementing it correctly has to do with the kind of indeterminate garbage disposal that I mention briefly