# 894 Chapter 21 Generic Collections: Functional Programming with LINQ/PLINQ

```
// generate output for each key in the sorted dictionary
// by iterating through the Keys property with a foreach statement
foreach (var key in dictionary.Keys)
{
    Console.WriteLine($"{key, -12}{dictionary[key],-12}");
}
Console.WriteLine($"\nsize:{dictionary.Count}");
```

Enter a string:
We, we are happy, we band of brothers

Sorted dictionary contains:
| Key Value |
|---|---|
| band 1 |
| brothers 1 |
| few, 2 |
| happy 1 |
| of 3 |

size: 6

**Fig. 21.4** App counts the number of occurrences of each word in a string and stores them in a generic sorted dictionary. (Part 3 of 3)

Lines 4–6 contain using directives for namespaces System (for class Console), System.Text.RegularExpressions (for class Regex) and System.Collections.Generic (for class SortedDictionary). The generic class SortedDictionary takes two arguments:

+   - the first specifies the type of key (i.e., string) and
- the second you the type of value (i.e., int).

+   Method CollectWords (lines 19–48) inputs a sentence and returns a SortedDictionary<string, int> in which the keys are the words in the sentence and the values are the number of times each word appears in the sentence.
- Method DisplayDictionary (lines 51–65) displays the SortedDictionary to it in column format.
- Method Main (lines 10–16) simply invokes CollectWords (line 13), passes the SortedDictionary<string, int> returned by CollectWords to DisplayDictionary in line 15.

Class SortedDictionary declares three methods:

# **CollectWords**

Method CollectWords (lines 19–48) begins by initializing local variable dictionary with a new SortedDictionary<string, int>(line 22). Lines 24–25 prompt the user and input a sentence as a string. We use static Split of class Regex (introduced in the