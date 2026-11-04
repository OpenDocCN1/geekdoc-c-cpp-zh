Other loops are often seen to read text, such as one that repeatedly calls the ReadLine method and checks for null to detect whether the end of the file has been reached. As expected, other methods, such as Read, ReadToEnd, and ReadBlock, can be found, all of which allow reading at different levels of granularity. For example, the Read method has two overloads, one of which returns a single character, whereas another takes in an array of characters to be populated:

```
```csharp
using (StreamReader sr = File.OpenText(@"..\\..\\Program.cs"))
{
    var buffer = new char[1024];
    int read = sr.Read(buffer, 0, buffer.Length);
    Console.WriteLine("{0} characters read", read);
}
```
```

Before studying the File class's capabilities any further, it's time to take a closer look at the concept of readers and writers, which find use outside file I/O as well.

# TextReader and TextWriter

The two classes we briefly encountered in the previous examples are subclasses of the TextReader and TextWriter classes. Using object-oriented programming at its best, these base classes offer virtual methods for a series of operations that can be applied in more than just the context of file I/O. In fact, on our much beloved Console class, you can find static properties called In and Out that expose a TextReader and a TextWriter:

```
```csharp
string line = Console.In.ReadLine();
Console.Out.WriteLine(line);
```
```

Console directly offers access to those common operations by providing shortcut methods on the class itself, but in reality a pair of reader and writer objects provides access to the Win32 console. In fact, those readers and writers can be substituted by means of Set methods, such as SetIn. This is quite handy when you're writing a console application that can receive input directly from the console (through user interaction) or from a file (for example, as specified through a command-line flag). Using the SetIn method, you can simply continue writing code against methods like Console.ReadLine while input is being redirected from another reader:

```
```csharp
static void Main(string[] args)
{
    if (args.Length == 1)
    {
        Console.SetIn(File.OpenText(args[0]));
    }

    string line;
    while ((line = Console.ReadLine()) != null)
```
```