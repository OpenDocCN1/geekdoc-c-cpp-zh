
method implementation, you iterate over the elements of the paths array and call `System.IO.Path.Combine()`. This method automatically combines the parts of the path, appropriately using the platform-specific directory-separator character. Note that `PathEx.Combine()` is identical to `Path.Combine()` except that `PathEx.Combine()` handles a variable number of parameters rather than simply two.

There are a few notable characteristics of the parameter array:

- The parameter array is not necessarily the only parameter on a method.
- The parameter array must be the last parameter in the method declaration. Since only the last parameter may be a parameter array, a method cannot have more than one parameter array.
- The caller can specify zero arguments that correspond to the parameter array parameter, which will result in an array of zero items being passed as the parameter array.
- Parameter arrays are type-safe: The arguments given must be compatible with the element type of the parameter array.
- The caller can use an explicit array rather than a comma-separated list of parameters. The resulting CIL code is identical.
- If the target method implementation requires a minimum number of parameters, those parameters should appear explicitly within the method declaration, forcing a compile error instead of relying on runtime error handling if required parameters are missing. For example, if you have a method that requires one or more integer arguments, declare the method as `int Max(int first, params int[] operands)` rather than as `int Max(params int[] operands)` so that at least one value is passed to `Max()`.

Using a parameter array, you can pass a variable number of arguments of the same type into a method. The section “Method Overloading,” which appears later in this chapter, discusses a means of supporting a variable number of arguments that are not necessarily of the same type.

## Guidelines

**DO** use parameter arrays when a method can handle any number—including zero—of additional arguments.

### Recursion

Calling a method **recursively** or implementing the method using recursion refers to use of a method that calls itself. Recursion is sometimes the simplest way to implement a particular algorithm. Listing 5.18 counts the lines of all the C# source files (*.cs) in a directory and its subdirectory.

```
Listing 5.18: Counting the Lines within *.cs Files, Given a Directory

using System.IO;

public static class LineCounter
{
    // Use the first argument as the directory
    // to search, or default to the current directory
    public static void Main(string[] args)
    {
        int totalLineCount = 0;
        string directory;
        if (args.Length > 0)
        {
            directory = args[0];
        }
        else
        {
            directory = Directory.GetCurrentDirectory();
        }
        totalLineCount = DirectoryCountLines(directory);
        System.Console.WriteLine(totalLineCount);
    }

    static int DirectoryCountLines(string directory)
    {
        int lineCount = 0;
        foreach (string file in
                 Directory.GetFiles(directory, "*.cs"))
        {
            lineCount += CountLines(file);
        }

        foreach (string subdirectory in
                 Directory.GetDirectories(directory))
        {
            lineCount += DirectoryCountLines(subdirectory);
        }

        return lineCount;
    }

    private static int CountLines(string file)
    {
        string line;
        int lineCount = 0;
        FileStream stream =
            new FileStream(file, FileMode.Open); 
        StreamReader reader = new StreamReader(stream);
        line = reader.ReadLine();

        while(line != null)
        {
            if (line.Trim() != "")
            {
                lineCount++;
            }
            line = reader.ReadLine();
        }

        reader.Close();  // Automatically closes the stream
        return lineCount;
    }
}
```

Output 5.9 shows the results of Listing 5.18.

### Output 5.9

104

The program begins by passing the first command-line argument to DirectoryCountLines() or by using the current directory if no argument is provided. This method first iterates through all the files in the current directory and totals the source code lines for each file. After processing each file in the directory, the code processes each subdirectory by passing the subdirectory back into the DirectoryCountLines() method, rerunning the method using the subdirectory. The same process is repeated recursively through each subdirectory until no more directories remain to process.

Readers unfamiliar with recursion may find it confusing at first. Regardless, it is often the simplest pattern to code, especially with hierarchical type data such as the filesystem. However, although it may be the most readable approach, it is generally not the fastest implementation. If performance becomes an issue, developers should seek an alternative solution to a recursive implementation. The choice generally hinges on balancing readability with performance.

1. This code could be improved with a using statement, a construct that we have avoided because it has not yet been introduced.

### BEGINNER TOPIC

### Infinite Recursion Error

A common programming error in recursive method implementations appears in the form of a stack overflow during program execution. This usually happens because of **infinite recursion**, in which the method continually calls back on itself, never reaching a point that triggers the end of the recursion. It is a good practice for programmers to review any method that uses recursion and to verify that the recursion calls are finite.

A common pattern for recursion using pseudocode is as follows:

```
M(x)
{
    if x is trivial
        return the result
    else
        a. Do some work to make the problem smaller
        b. Recursively call M to solve the smaller problem
        c. Compute the result based on a. and b.
        return the result
}
```

Things go wrong when this pattern is not followed. For example, if you don't make the problem smaller or if you don't handle all possible "smallest" cases, the recursion never terminates.

### Method Overloading

Listing 5.18 called *DirectoryCountLines()*, which counted the lines of `*.cs` files. However, if you want to count code in `*.h`/`.cpp` files or in `*.vb` files, *DirectoryCountLines()* will not work. Instead, you need a method that takes the file extension but still keeps the existing method definition so that it handles `*.cs` files by default.

All methods within a class must have a unique signature, and C# defines uniqueness by variation in the method name, parameter data types, or number of parameters. This does not include method return data types; defining two methods that differ only in their return data types will cause a compile error. This is true even if the return type is two different tuples. **Method overloading** occurs when a class has two or more methods with the same name and the parameter count and/or data types vary between the overloaded methods.

![](img/ef6a8a417630b222bfb3f3b949facff0_254_0.png)

Method overloading is a type of **operational polymorphism**. Polymorphism occurs when the same logical operation takes on many (“poly”) forms (“morphs”) because the data varies. Calling WriteLine() and passing a format string along with some parameters is implemented differently than calling WriteLine() and specifying an integer. However, logically, to the caller, the method takes care of writing the data, and it is somewhat irrelevant how the internal implementation occurs. Listing 5.19 provides an example, and Output 5.10 shows the results.

### LISTING 5.19: Counting the Lines within .cs Files Using Overloading

```
using System.IO;

public static class LineCounter
{
public static void Main(string[] args)
{
int totalLinesCount;
if (args.Length > 1)
{
totalLinesCount =
DirectoryCountLines(args[0], args[1]);
}
if (args.Length > 0)
{
totalLinesCount = DirectoryCountLines(args[0]);
}
else
{
totalLinesCount = DirectoryCountLines();
}
System.Console.WriteLine(totalLinesCount);
}
}
```
