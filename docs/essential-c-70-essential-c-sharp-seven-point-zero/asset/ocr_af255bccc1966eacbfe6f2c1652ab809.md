```
```csharp
System.Console.WriteLine();
System.Console.WriteLine(
    $"{ \"First Element\",-20 }{t{ \"Last Element\",-20 }");
System.Console.WriteLine(
    $"{ \"-----------\",-20 }{t{ \"-----------\",-20 }");
System.Console.WriteLine(
    $"{ languages[0],-20 }\t{ languages[languages.Length-1],-20 "});
System.Array.Reverse(languages);
System.Console.WriteLine(
    $"{ languages[0],-20 }\t{ languages[languages.Length-1],-20 }");
// Note this does not remove all items from the array.
// Rather, it sets each item to the type's default value.
System.Array.Clear(languages, 0, languages.Length);
System.Console.WriteLine(
    $"{ languages[0],-20 }\t{ languages[languages.Length-1],-20 }");
System.Console.WriteLine(
    $"After clearing, the array size is: { languages.Length }");
```

```

The results of Listing 3.25 are shown in Output 3.2.

# Output 3.2

```
The wave of the future, COBOL, is at index 2.
```
First Element       Last Element
----------          ----------
C#                  Visual Basic
Visual Basic         C#
```
After clearing, the array size is: 9
```

Access to these methods is obtained through the System.Array class. For the most part, using these methods is self-explanatory, except for two noteworthy items:

+   - Before using the BinarySearch( ) method, it is important to sort the array. If values are not sorted in increasing order, the incorrect index may be returned. If the search element does not exist, the value returned is negative. (Using the complement operator, \~index, returns the first index, if any, that is larger than the searched value.)