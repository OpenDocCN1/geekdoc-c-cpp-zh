
## Length

You can obtain the length of an array, as shown in Listing 3.22.

**LISTING 3.22: Retrieving the Length of an Array**

```
Console.WriteLine(
    $"There are { languages.Length } languages in the array.");
```

Arrays have a fixed length; they are bound such that the length cannot be changed without re-creating the array. Furthermore, overstepping the **bounds** (or length) of the array will cause the runtime to report an error. This can occur when you attempt to access (either retrieve or assign) the array with an index for which no element exists in the array. Such an error frequently occurs when you use the array length as an index into the array, as shown in Listing 3.23.

**LISTING 3.23: Accessing Outside the Bounds of an Array, Throwing an Exception**

```
string languages = new string[9];
...
// RUNTIME ERROR: index out of bounds – should
// be 8 for the last element
languages[4] = languages[9];
```

![](img/ef6a8a417630b222bfb3f3b949facff0_135_0.png)

![](img/ef6a8a417630b222bfb3f3b949facff0_135_1.png)

It is a good practice to use `Length` in place of the hardcoded array size. To use `Length` as an index, for example, it is necessary to subtract 1 to avoid an out-of-bounds error (see Listing 3.24).

**LISTING 3.24: Using Length - 1 in the Array Index**

```csharp
string languages = new string[9];
...
languages[4] = languages[languages.Length - 1];
```

To avoid overstepping the bounds on an array, use a length check to verify that the array has a length greater than 0, and use `Length - 1` in place of a hardcoded value when accessing the last item in the array (see Listing 3.24).

`Length` returns the total number of elements in an array. Therefore, if you had a multidimensional array such as `bool cells[ , ]` of size 2 × 3 × 3, `Length` would return the total number of elements, 18.

For a jagged array, `Length` returns the number of elements in the first array. Because a jagged array is an array of arrays, `Length` evaluates only the outside containing array and returns its element count, regardless of what is inside the internal arrays.

### More Array Methods

Arrays include additional methods for manipulating the elements within the array—for example, `Sort()`, `BinarySearch()`, `Reverse()`, and `Clear()` (see Listing 3.25).

**LISTING 3.25: Additional Array Methods**

```csharp
class ProgrammingLanguages
{
    static void Main()
    {
        string[] languages = new string[]{
            "C#", "COBOL", "Java",
            "C++", "Visual Basic", "Pascal",
            "Fortran", "Lisp", "J#"};

        System.Array.Sort(languages);

        string searchString = "COBOL";
        int index = System.Array.BinarySearch(
            languages, searchString);
        System.Console.WriteLine(
            "The wave of the future, "
            + $"{ searchString }, is at index { index }");

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
    }
}
```

The results of Listing 3.25 are shown in Output 3.2.

**OUTPUT 3.2**

```
The wave of the future, COBOL, is at index 2.
First Element       Last Element
----------          ----------
C#                  Visual Basic
Visual Basic         C#
After clearing, the array size is: 9
```

Access to these methods is obtained through the `System.Array` class. For the most part, using these methods is self-explanatory, except for two noteworthy items:

- Before using the `BinarySearch( )` method, it is important to sort the array. If values are not sorted in increasing order, the incorrect index may be returned. If the search element does not exist, the value returned is negative. (Using the complement operator, `~index`, returns the first index, if any, that is larger than the searched value.)
- The `Clear()` method does not remove elements of the array and does not set the length to zero. The array size is fixed and cannot be modified. Therefore, the `Clear()` method sets each element in the array to its default value (`false`, `0`, or `null`). This explains why `Console.WriteLine()` creates a blank line when writing out the array after `Clear()` is called.

### Language Contrast: Visual Basic—Redimensioning Arrays

Visual Basic includes a `ReDim` statement for changing the number of items in an array. Although there is no equivalent C#-specific keyword, there is a method available in .NET 2.0 that will re-create the array and then copy all the elements over to the new array. This method is called `System.Array.Resize`.

### Array Instance Methods

Like strings, arrays have instance members that are accessed not from the data type but directly from the variable. `Length` is an example of an instance member because access to `Length` is through the array variable, not the class. Other significant instance members are `GetLength()`, `Rank`, and `Clone()`.

Retrieving the length of a particular dimension does not require the `Length` property. To retrieve the size of a particular rank, an array includes a `GetLength()` instance method. When calling this method, it is necessary to specify the rank whose length will be returned (see Listing 3.26).

**LISTING 3.26: Retrieving a Particular Dimension's Size**

```csharp
bool[,] cells;
cells = new bool[2,3,3];
System.Console.WriteLine(cells.GetLength(0));   // Displays 2
```

The results of Listing 3.26 appear in Output 3.3.

**OUTPUT 3.3**

2

Listing 3.26 displays 2 because that is the number of elements in the first dimension.

It is also possible to retrieve the entire array's rank by accessing the array's `Rank` member. `cells.Rank`, for example, will return 3.

By default, assigning one array variable to another copies only the array reference, not the individual elements of the array. To make an entirely new copy of the array, use the array's `Clone()` method. The `Clone()` method will return a copy of the array; changing any of the members of this new array will not affect the members of the original array.

### Strings as Arrays

Variables of type `string` are accessible like an array of characters. For example, to retrieve the fourth character of a string called `palindrome`, you can call `palindrome[3]`. Note, however, that because strings are immutable, it is not possible to assign particular characters within a string. C#, therefore, would not allow `palindrome[3]='a'`, where `palindrome` is declared as a string. Listing 3.27 uses the array accessor to determine whether an argument on the command line is an option, where an option is identified by a dash as the first character.

**LISTING 3.27: Looking for Command-Line Options**

```csharp
string[] args;
...
if(args[0][0] == '-')
{
    // This parameter is an option
}
```

This snippet uses the `if` statement, which is covered in Chapter 4. In addition, it presents an interesting example because you use the array accessor to retrieve the first element in the array of strings, `args`. Following the first array accessor is a second one, which retrieves the first character of the string. The code, therefore, is equivalent to that shown in Listing 3.28.

**LISTING 3.28: Looking for Command-Line Options (Simplified)**

```csharp
string[] args;
...
string arg = args[0];
if(arg[0] == '-')
{
    // This parameter is an option
}
```
