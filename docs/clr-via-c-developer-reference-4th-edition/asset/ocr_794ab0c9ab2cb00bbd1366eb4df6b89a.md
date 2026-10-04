# Using a Type That Wraps a Native Resource

Now you know how to define a SafeHandle-derived class that wraps a native resource, let's take a look at how a developer uses it. Let's start talking about the common System.IO.FileStream class. The FileStream class offers the ability to open a file, read bytes from the file, write bytes to the file, and close it. When a FileStream object is constructed, the Win32 CreateFile function is called, the returned handle is saved in a SafeHandle object, and a reference to this object is maintained via a private field in the FileStream object. The FileStream class also offers several additional properties (such as Length, Position, CanRead) and methods (such as Read, Write, Flush).

Let's say you want to write code that creates a temporary file, writes some bytes to the file, and then deletes it. You might start writing the code like this:

```
using System;
using System.IO;
public static class Program {
public static void Main() {// Create the bytes to write to the temporary file.
  Byte[] bytesToWrite = new Byte[] { 1, 2, 3, 4, 5 };

  // Create the temporary file.
  FileStream fs = new FileStream("Temp.dat", FileMode.Create);

  // Write the bytes to the temporary file.
  fs.Write(bytesToWrite, 0, bytesToWrite.Length);

  // Delete the temporary file.
  File.Delete("Temp.dat"); // Throws an IOException
}
```

Unfortunately, if you build and run this code, it might work, but most likely it won't. The problem is that the call to File's static Delete method requests that Windows delete a file while it is still open. So Delete throws a System.IO.IOException with the following string message: The process cannot access the file "Temp.dat" because it is being used by another process.

Be aware that in some cases, the file might actually be deleted! If another thread caused a garbage collection to start after the call to Write and before the call to Delete, the FileStream's SafeFileHandle would have its Finalize method called, which would close the file and allow Delete to work. The likelihood of this situation is extremely rare, however, and therefore the previous code will fail more than 99 percent of the time.