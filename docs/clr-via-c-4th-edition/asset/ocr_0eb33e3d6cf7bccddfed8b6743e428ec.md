Keep in mind that calling Dispose is not required to guarantee native resource cleanup. Native resource cleanup will always happen eventually; calling Dispose lets you control when that cleanup happens. Also, calling Dispose does not delete the managed object from the managed heap. The only way to reclaim memory in the managed heap is for a garbage collection to kick in. This means you can still call methods on the managed object even after you dispose of any native resources it may have been using.

The following code calls the Write method after the file is closed, attempting to write more bytes to the file. Obviously, the bytes can't be written, and when the code executes, the second call to the Write method throws a System.ObjectDisposedException exception with the following string message: Cannot access a closed file.

```
~~~csharp
using System;
using System.IO;

public static class Program {
    public static void Main() {
        // Create the bytes to write to the temporary file.
        Byte[] bytesToWrite = new Byte[] { 1, 2, 3, 4, 5 };

        // Create the temporary file.
        FileStream fs = new FileStream("Temp.dat", FileMode.Create);

        // Write the bytes to the temporary file.
        fs.Write(bytesToWrite, 0, bytesToWrite.Length);

        // Explicitly close the file when finished writing to it.
        fs.Dispose();

        // Try to write to the file after closing it.
        fs.Write(bytesToWrite, 0, bytesToWrite.Length);   // Throws ObjectDisposedException

        // Delete the temporary file.
        File.Delete("Temp.dat");
    }
}
~~~
```

Note that no memory corruption occurs here because the memory for the FileStream object still exists in the managed heap; it's just that the object can't successfully execute its methods after it is explicitly disposed.

> > **Important** When defining your own type that implements the IDisposable interface, be sure to write code in all of your methods and properties to throw a System.ObjectDisposedException if the object has been explicitly cleaned up. A Dispose method should never throw an exception; if it's called multiple times, it should just return.