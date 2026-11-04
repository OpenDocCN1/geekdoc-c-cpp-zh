Here, obj is an expression that must evaluate to an object that implements the System.IDisposable interface. It specifies a variable that will be used inside the using block. In the first form, the object is declared outside the using statement. In the second form, the object is declared within the using statement. When the block concludes, the Dispose() method (defined by the System.IDisposable interface) will be called on obj. Dispose() is called even if the using block ends because of an exception. Thus, a using statement provides a means by which objects are automatically disposed when they are no longer needed. Remember, the using statement applies only to objects that implement the System.IDisposable interface.

Here is an example of each form of the using statement:

```
// Demonstrate using statement.
using System;
using System.IO;

class UsingDemo {
  static void Main() {
    try {
      StreamReader sr = new StreamReader("test.txt");

      // Use object inside using statement.
      using(sr) {
        // ...
      }
    } catch(IOException exc) {
      // ...
    }

    try {
      // Create a StreamReader inside the using statement.
      using(StreamReader sr2 = new StreamReader("test.txt")) {
        // ...
      }
    } catch(IOException exc) {
      // ...
    }
  }
}
```

The class StreamReader implements the IDisposable interface (through its base class TextReader). Thus, it can be used in a using statement. When the using statement ends, Dispose() is automatically called on the stream variable, thus closing the stream.

As the preceding example illustrates, using is particularly useful when working with files because the file is automatically closed at the end of the using block, even if the block ends because of an exception. As a result, closing a file via using often simplifies file-handling code.

# extern

The extern keyword has two uses. Each is examined here.