```
static void Main(string[] args)
{
    Console.Write("Hello, ");
    for (int i = 0; i < args.Length; i++)
    {
        Console.Write("{0} ", args[i]);
    }
    Console.Write("! This is my first C# program!");
    Console.ReadLine();
    return;
}

/// <summary>
/// Adds two numbers and returns the result
/// </summary>
/// <param name="num1">Number 1</param>
/// <param name="num2">Number 2</param>
/// <returns>Sum of Number 1 and 2</returns>
private int AddNumbers(int num1, int num2)
{
    //---implementations here---
}
```

To enable generation of the XML document containing the XML comments, right-click the project name in Solution Explorer and select Properties.

> You can also generate the XML documentation file using the csc.exe compiler at the command prompt using the /doc option:
> 
> csc Program.cs /doc:HelloWorld.xml

In the Build tab, tick the XML Documentation File checkbox and use the default path suggested: bin\Debug\HelloWorld.XML (see Figure 3-7).