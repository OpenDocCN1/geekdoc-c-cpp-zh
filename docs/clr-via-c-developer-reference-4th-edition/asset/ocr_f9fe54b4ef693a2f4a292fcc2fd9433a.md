Classes that allow the consumer to control the lifetime of native resources wraps implement the IDisposable interface, which looks like this.

```
public interface IDisposable {
    void Dispose();
}}
```

> **Important** If a class defines a field in which the field's type implements the dispose pattern, the class itself should also implement the dispose pattern. The Dispose method should dispose of the object referred to by the field. This allows someone using the class to call Dispose on it, which in turn releases the resources used by the itself.

Fortunately, the FileStream class implements the IDisposable interface and its implementation calls Dispose on the FileStream object's private SafeFileHandle handle. Now we can modify our code to explicitly close the file when we want to avoid waiting for some GC to happen in the future. Here's the corrected source code.

```
using System;
using System.IO;

public static class Program {
    public static void Main() {
        // Create the bytes to write to the temporary file.
        Byte[] bytesToWrite = new byte[] { 1, 2, 3, 4, 5 };

        // Create the temporary file.
        FileStream fs = new FileStream("Temp.dat", FileMode.Create);

        // Write the bytes to the temporary file.
        fs.Write(bytesToWrite, 0, bytesToWrite.Length);

        // Explicitly close the file when writing to it.
        fs.Dispose();

        // Delete the temporary file.
        File.Delete("Temp.dat"); // This always works now.
}
```

Now, when File's Delete method is called, Windows sees that the file isn' open and successfully deletes it.