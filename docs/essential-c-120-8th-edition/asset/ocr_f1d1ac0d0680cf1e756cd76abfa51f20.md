simple conditional branching (if) and unconditional branching (goto) statements for most of their control flow needs. Programs were often hard to understand. The continued existence of a goto statement within C# seems like an anachronism to many experienced programmers. However, C# supports goto, and it is the only method for supporting fall-through within a statement. In Listing 4.55, if the /out option is set, code execution jumps to the default case using goto statement, and similarly for /f. Output 4.26 provides an example of the program executing.

# Listing 4.55: Demonstrating a switch with goto Statements

```
// ...
public static void Main(string[] args)
{
    bool isOutputSet = false;
    bool isFiltered = false;
    bool isRecursive = false;

    foreach(string option in args)
    {
        switch(option)
        {
            case "out":
                isOutputSet = true;
                isFiltered = false;
                // ...
                goto default;
            case "/f":
                isFiltered = true;
                isRecursive = false;
                // ...
                goto default;
        }
        default:
        if(isRecursive)
        {
            // Recursse down the hierarchy
            Console.WriteLine("Recursing...");
            // ...
        }
        else if(isFiltered)
        {
            // Add option to list of filters
            Console.WriteLine("Filtering...");
            // ...
        }
}
```