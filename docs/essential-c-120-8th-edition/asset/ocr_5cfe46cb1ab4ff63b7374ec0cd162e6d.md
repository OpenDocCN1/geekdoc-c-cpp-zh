# Code Blocks, Scopes, and Declaration Spaces 165

LISTING 4.28: Variables Inaccessible outside Their Scope

```
string playerCount;
Console.Write(
    "Enter the number of players (1 or 2):*");
playerCount = Console.ReadLine();
if (playerCount != "1" && playerCount != "2")
{
    string message =
    "You entered an invalid number of players.";
}
else
{
    // ...
}
// ERROR: message is not in scope:
Console.WriteLine(message);
```

# OUTPUT 4.15

...\Program.cs(18,26): error CS0103: The name 'message' does not exist in the current context

The declaration space in which a local variable's name must be unique encompasses all the code blocks textually enclosed within the block that originally declared the local. The C# compiler prevents the name of a local variable declared immediately within a method code block (or as a parameter) from being reused within a child code block. In Listing 4.28, args and playerCount are declared within the method code block, they cannot be declared again anywhere within the method.

The name message refers to this local variable throughout the scope of the local variable—that is, the block immediately enclosing the declaration. Similarly, playerCount refers to the same variable throughout the block containing the declaration, including within both of the child blocks that are the consequence and the alternative of the if statement.