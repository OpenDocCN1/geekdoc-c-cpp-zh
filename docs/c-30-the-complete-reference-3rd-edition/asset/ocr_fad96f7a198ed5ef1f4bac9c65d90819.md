Here, str is the string that will be read from.

StringWriter defines several constructors. Here is the one that we will use:

StringWriter()

This constructor creates a writer that will put its output into a string. This string (in the form of a StringBuilder) is automatically created by StringWriter. You can obtain the contents of this string by calling ToString().

Here is an example that uses StringReader and StringWriter:

```
// Demonstrate StringReader and StringWriter.
using System;
using System.IO;

class StrRdrDemo {
  static void Main() {
    // Create a StringWriter.
    StringWriter strwtr = new StringWriter();

    // Write to StringWriter.
    for(int i=0; i < 10; i++)
      strwtr.WriteLine("This is i: " + i);

    // Create a StringReader.
    StringReader strrdr = new StringReader(strwtr.ToString());

    // Now, read from StringReader.
    string str = strrdr.ReadLine();
    while(str != null) {
      str = strrdr.ReadLine();
      Console.WriteLine(str);
    }
  }
}
```

The output is shown here:

```
This is i: 1
This is i: 2
This is i: 3
This is i: 4
This is i: 5
This is i: 6
This is i: 7
This is i: 8
This is i: 9
```

The program first creates a StringWriter called strwtr and outputs to it using WriteLine(). Next, it creates a StringReader using the string contained in strwtr. This string is obtained by calling ToString() on strwtr. Finally, the contents of this string are read using ReadLine().