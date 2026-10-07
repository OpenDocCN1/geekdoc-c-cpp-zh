
# Pattern Matching 435

```cs
// Discard last name portion of tuple
,
{
  // Property of Princess Buttercup tuple
  FirstName: string buttercupFirstName
  Console.WriteLine("$ { inigoFirstNameLength }, { buttercupFirstName }}");
}
else {
  // ...
}
// ...
```

In this example, couple is of the following type:

(Person, (string FirstName, string LastName))

As such, the first match occurs on the outer tuple, (inigo, buttercup). Next, positional pattern matching is used against inigo, leveraging the Person deconstructor. This selects a (FirstName, LastName) tuple, from which property pattern matching is used to extract the Length of the inigo.FirstName value. The LastName portion of the positional pattern matching is discarded with an underscore. Finally, property pattern matching is used to select buttercup.FirstName.

While pattern matching is a powerful means to select data, it is not without a caution: Be mindful of the comments of Listing 7.32, it is likely challenging to understand the code. Without them, it would be even harder:

```cs
if (couple is ( { Length: int inigoFirstNameLength }, _ ), { FirstName: string buttercupFirstName }}) { ...}
```

Even so, where pattern matching really proves useful is in switch statements and expressions.

# List Patterns (C# 11.0)

One important new feature in C# 11 is the introduction of list patterns. These enable pattern matching over a list of items such as an array. As such, you can use any type of pattern matching on the elements within the list. 7.33 demonstrates the feature to parse the args parameter of the Main method.

LISTING 7.33: Pattern Matching within a switch Expression

```cs
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

# Pattern Matching

```cs
break;
}
private static bool EvaluateOption(string option, string[] args) =>
    (option, args) switch
{
    ("cat" or "c", [string fileName]) =>
        CatalogFile(fileName),
    ("copy", [string sourceFile, string targetFile]) =>
        CopyFile(sourceFile, targetFile),
    _ => false
};
```

```cs
private static bool CopyFile(object sourceFile, string targetFile)
{
    Console.WriteLine($"'{sourceFile}' '{targetFile}'...");
    return true;
}
```

The first case in Listing 7.33 looks for the text "-help" as the first and only element of the args array. If there is no match, the remainder of the list expression matches on a first element that starts with / or - followed by ? or h. The later part of the list pattern looks for exactly two characters (because a string is an array of characters) as identified by the comma, (.) within the expression, separating the prefix from the single character expression:

```cs
['/' or '-', 'h' or '?']
```

The next two cases evaluate the first element of args as well, determining whether the first character is a / or a -, in the third case, whether the first element of args starts with --. In both cases, if there is a match, args[] is assigned to the option variable. Unfortunately, there is no way to capture the remaining elements of the list into a variable. List matching always looks for exact number of elements. For this reason, when EvaluateOptions(), we use range [1..] to pass the remaining elements. (see://essentialsharp.com/arrays) for examples.

The fourth case uses [] to identify a list with zero elements. In this example, it is redundant because the default case also captures the remaining arguments. Within EvaluateOptions method of Listing 7.33, we use a tuple to first evaluate the command. For "cat" match expression, it looks for one item, whereas for "copy" match expression, it looks for exactly two items. In both cases, it captures the array into variables. There is a lot of power in pattern matching, and because it works with strings, it enables simple scenarios without resorting to regular expressions.

# Avoid Pattern Matching When Polymorphism Is Possible

Although pattern matching capability is important, you should consider issues related to polymorphism prior to using pattern matching. Polymorphism supports the expansion of data types without requiring modification. For example, placing a member like Name in the base class PdaItem and then working with values derived from PdaItem is preferable to using pattern matching to address newly introduced type. Regardless, polymorphism is not always possible, and when it isn't, pattern matching, specifically something like property matching, provides a good alternative.

One scenario where polymorphism fails when no object hierarchy matches your goals—if you are working with classes that are part of unrelated systems, for example. Furthermore, it is assumed the code requiring polymorphism cannot be modified. Working with the dates in 7.33 is one such example. A second scenario is when functionality you're adding isn't part of the abstraction for these classes. For example, the toll paid by drivers changes for different types of vehicles traveling on a toll road, but the toll isn’t a core function of the vehicle.

# ADVANCED TOPIC

# Using the as Operator

In addition to the operator, C# has an as operator. Originally, the as operator offered an advantage over the is operator: It not only checks whether operand is of a specific type also attempts a conversion to the particular data type and assigns null if the source type is not inherently (within the inheritance chain) of the target type. Furthermore, it provides an advantage over casting because it won’t throw an exception. Listing 7.34 demonstrates the use of the as operator.

Listing 7.34: Data Conversion Using the as Operator

```cs
public class PdaItem {
    protected Guid ObjectKey { get; }
    // ...
}
public class Contact : PdaItem {
    // ...
    public Contact(string name) => Name = name;
    static public Contact Load(PdaItem pdaItem) {
        #pragma warning disable IDE0019 // Use pattern matching
        Contact? contact = pdaItem as Contact;
        #pragma warning restore IDE0019 // Use pattern matching
        if (contact != null) {
            System.Diagnostics.Trace.WriteLine($"ObjectKey: {contact.ObjectKey}");
            return (Contact)pdaItem;
        }
    else {
        throw new ArgumentException("Item is not contact");
    }
}
```
