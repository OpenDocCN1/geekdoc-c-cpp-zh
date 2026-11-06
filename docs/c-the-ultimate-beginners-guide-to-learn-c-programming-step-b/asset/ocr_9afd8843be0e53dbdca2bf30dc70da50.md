+   - public override int Read()- this method will read the next character in an input stream then advance the position of the character by 1.

Let us demonstrate how we can use this class to read from a file named *names.txt*:

```
```csharp
using System.IO;

using System;

namespace IOApplication {
    class MyProgram {
        static void Main(string[] args) {
            try {
                // Create a StreamReader instance for reading from a file.
                // The using statement will close the StreamReader.
                using (StreamReader sr = new StreamReader("c:/names.txt")) {
                    string line;

                    // Read the show lines from the file until
                    // you reach the end of the file.
                    while ((line = sr.ReadLine()) != null) {
                        Console.WriteLine(line);
                    }
                }
            } catch (Exception exception) {
                // Information the user about what went wrong
                Console.WriteLine("File couldn't be read:");
                Console.WriteLine(exception.Message);
            }
            Console.ReadKey();
        }
    }
}
```
```