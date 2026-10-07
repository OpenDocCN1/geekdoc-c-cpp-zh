# List Patterns (C# 11.0)

One important new feature in C# 11 is the introduction of list patterns. These enable pattern matching over a list of items such as an array. As such, you can use any type of pattern matching on the elements within the list. 7.33 demonstrates the feature to parse the args parameter of the Main method.

LISTING 7.33: Pattern Matching within a switch Expression

```
public static void Main(string[] args)
{
    // For simplicity, options are assumed
    // to all be lower case.

    // The first argument is the option and is
    // identified by a '/', '-', or '--' prefix.
    switch (args)
    {
        case "--" or ['/' or '-', 'h' or '?']:
            // e.help, /h, -h, ?, -?
            DisplayHelp();
            break;
        case ['/' or '-', char option], ..]:
            // Option begins with '/', '-' and has 0 or more arguments.
            if(EvaluateOption("${option}", args[1..]))
            {
                DisplayHelp();
            }
            break;
        case ['-', ..] option, ..:
            // Option begins with "--" and has 0 or more arguments.
            if(EvaluateOption(option[2..], args[1..]))
            {
                DisplayHelp();
            }
            break;

        // The following cases are redundant with default
        // but provided for demonstration purposes.
        case []:
            // No command line arguments
    }

    default:
        DisplayHelp();
}
```