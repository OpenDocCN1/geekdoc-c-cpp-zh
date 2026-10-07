# Pattern Matching

```
break;
}
private static bool EvaluateOption(string option, string[] args) =>
    (option, args) switch
{
    ("cat" or "c", [string fileName]) =>
        CatalogFile(fileName),
    ("copy", [string sourceFile, string targetFile]) =>
        CopyFile(sourceFile, targetFile),
    => false
};
```

```
private static bool CopyFile(object sourceFile, string targetFile)
{
    Console.WriteLine($"'{sourceFile}' '{targetFile}'...");
    return true;
}
```

The first case in Listing 7.33 looks for the text "-help" as the first and only element of the args array. If there is no match, the remainder of the list expression matches on a first element that starts with / or - followed by ? or h. The later part of the list pattern looks for exactly two characters (because a string is an array of characters) as identified by the comma, (.) within the expression, separating the prefix from the single character expression:

```
['/' or '-', 'h' or '?']
```

The next two cases evaluate the first element of args as well, determining whether the first character is a / or a -, in the third case, whether the first element of args starts with --. In both cases, if there is a match, args[] is assigned to the option variable. Unfortunately, there is no way to capture the remaining elements of the list into a variable. List matching always looks for an exact number of elements or allows for .. to mean no further evaluation of the remaining elements is required. For this reason, when invoking EvaluateOptions(), we use the range args[1..] to pass all the elements in args except the first one (see Chapter 3 (https://essentialsharp.com/arrays) for examples on ranges).