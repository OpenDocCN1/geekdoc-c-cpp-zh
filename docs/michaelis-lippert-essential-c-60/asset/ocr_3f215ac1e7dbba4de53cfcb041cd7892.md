In summary, a scope is used to determine what thing a name refers to; a declaration space determines when two things declared with the same name conflict with each other. In Listing 3.27, declaring the local variable message inside the block statement embedded in the if statement restricts its scope to the block statement only; the local variable is “out of scope” when its name is used later on in the method. To avoid an error, you must declare the variable outside the block.

# LISTING 3.27: Variables Inaccessible outside Their Scope

```
class Program
{
    static void Main(string[] args)
    {
        int playerCount;
        System.Console.Write(
            "Enter the number of players (1 or 2):");
        playerCount = int.Parse(System.Console.ReadLine());
        if (playerCount != 1 && playerCount != 2)
        {
            string message =
                "You entered an invalid number of players.";
        }
        else
        {
            // ...
        }
        // Error: message is not in scope.
        System.Console.WriteLine(message);
    }
}
```

Output 3.15 shows the results of Listing 3.27.

# OUTPUT 3.15

```
...
...\Program.cs(18,26): error CS0103: The name 'message' does not exist in the current context
```

The declaration space in which a local variable’s name must be unique encompasses all the child code blocks textually enclosed within the block that originally declared the local. The C# compiler prevents the name of a local variable declared immediately within a method code block (or as a