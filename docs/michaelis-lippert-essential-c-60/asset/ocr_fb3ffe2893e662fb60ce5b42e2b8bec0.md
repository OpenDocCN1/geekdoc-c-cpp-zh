# Guidelines

DO favor use of read-only automatically implemented properties in C# 6.0 (or later) over defining read-only fields.

DO use public static readonly modified fields for predefined object instances prior to C# 6.0.

AVOID changing a public readonly modified field in pre-C# 6.0 to a read-only automatically implemented property in C# 6.0 (or later) if version API compatibility is required.

# Nested Classes

In addition to defining methods and fields within a class, it is possible to define a class within a class. Such classes are called nested classes. You use a nested class when the class makes little sense outside the context of its containing class.

Consider a class that handles the command-line options of a program. Such a class is generally unique to each program, so there is no reason to make a CommandLine class accessible from outside the class that contains Main(). Listing 5.45 demonstrates such a nested class.

# LISTING 5.45: Defining a Nested Class

```
// CommandLine is nested within Program
class Program
{
    // Define a nested class for processing the command line.
    private class CommandLine
    {
        public CommandLine(string[] arguments)
        {
            for(int argumentCounter=0;
                argumentCounter<arguments.Length;
                argumentCounter++)
            {
                switch (argumentCounter)
                {
                    case 0:
                        Action = arguments[0].ToLower();
                        break;
                    case 1:
                        Id = arguments[1];
                        break;
```