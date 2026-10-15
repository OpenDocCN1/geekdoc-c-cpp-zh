
The square bracket notation is also used to store data into an array. Listing 2.45 switches the order of "C++" and "Java".

## LISTING 2.45: Swapping Data between Positions in an Array

```
string[] languages = new string[9]{
    "C#", "COBOL", "Java",
    "C++", "Visual Basic", "Pascal",
    "Fortran", "Lisp", "J#"};
// Save "C++" to variable called Language.
string language = languages[3];
// Assign "Java" to the C++ position.
languages[3] = languages[2];
// Assign Language to location of "Java".
languages[2] = language;
```

For multidimensional arrays, an element is identified with an index for each dimension, as shown in Listing 2.46.

## LISTING 2.46: Initializing a Two-Dimensional Array of Integers

```
int[,] cells = {
    {1, 0, 2},
    {0, 2, 0},
    {1, 2, 1}
};
// Set the winning tic-tac-toe move to be player 1.
cells[1,0] = 1;
```

Jagged array element assignment is slightly different because it is consistent with the jagged array declaration. The first element is an array within the array of arrays; the second index specifies the item within the selected array element (see Listing 2.47).

## LISTING 2.47: Declaring a Jagged Array

```
int[][] cells = {
    new int[]{1, 0, 2},
    new int[]{0, 2, 0},
    new int[]{1, 2, 1}
};

cells[1][0] = 1;
// ...
```

## Length

You can obtain the length of an array, as shown in Listing 2.48.

```
Console.WriteLine(
    $"There are { languages.Length } languages in the array.");
```

Arrays have a fixed length; they are bound such that the length cannot be changed without re-creating the array. Furthermore, overstepping the bounds (or length) of the array will cause the runtime to report an error. This can occur when you attempt to access (either retrieve or assign) the array with an index for which no element exists in the array. Such an error frequently occurs when you use the array length as an index into the array, as shown in Listing 2.49.

```
string languages = new string[9];
...
// RUNTIME ERROR: index out of bounds - should
// be 8 for the last element
languages[4] = languages[9];
```

> **NOTE**
> 
> The Length member returns the number of items in the array, not the highest index. The Length member for the languages variable is 9, but the highest index for the languages variable is 8, because that is how far it is from the start.

It is a good practice to use Length in place of the hardcoded array size. To use Length as an index, for example, it is necessary to subtract 1 to avoid an out-of-bounds error (see Listing 2.50).

```
string languages = new string[9];
...
languages[4] = languages[languages.Length - 1];
```

To avoid overstepping the bounds on an array, use a length check to verify that the array has a length greater than 0 and use Length - 1 in place of a hardcoded value when accessing the last item in the array (see Listing 2.50). Length returns the total number of elements in an array. Therefore, if you had a multidimensional array such as `bool cells[,,]` of size 2 × 3 × 3, Length would return the total number of elements, 18.

For a jagged array, Length returns the number of elements in the first array. Because a jagged array is an array of arrays, Length evaluates only the outside, containing array and returns its element count, regardless of what is inside the internal arrays.

## Language Contrast: C++—Buffer Overflow Bugs

Unmanaged C++ does not always check whether you overstep the bounds on an array. Not only can this be difficult to debug, but making this mistake can also result in a potential security error called a **buffer overrun**. In contrast, the Common Language Runtime protects all C# (and Managed C++) code from overstepping array bounds, virtually eliminating the possibility of a buffer overrun issue in managed code.

## More Array Methods

Arrays include additional methods for manipulating the elements within the array—for example, Sort(), BinarySearch(), Reverse(), and Clear() (see Listing 2.51).

```
```csharp
class ProgrammingLanguages
{
    static void Main()
    {
        string[] languages = new string[]
        {
            "C#", "COBOL", "Java",
            "C++", "Visual Basic", "Pascal",
            "Fortran", "Lisp", "J#"
        };

        System.Array.Sort(languages);

        string searchString = "COBOL";
```

```
int index = System.Array.BinarySearch(
    languages, searchString);
System.Console.WriteLine(
    "The wave of the future, "
    + $"{ searchString }, is at index { index }.");

System.Console.WriteLine();
System.Console.WriteLine(
    $"{ "First Element",-20 }\t{ "Last Element",-20 }");
System.Console.WriteLine(
    $"{ "------------",-20 }\t{ "------------",-20 }");
System.Console.WriteLine(
    $"{ languages[0],-20 }\t{ languages[languages.Length-1],-20 }");
System.Array.Reverse(languages);
System.Console.WriteLine(
    $"{ languages[0],-20 }\t{ languages[languages.Length-1],-20 }");
// Note this does not remove all items from the array.
// Rather it sets each item to the type's default value.
System.Array.Clear(languages, 0, languages.Length);
System.Console.WriteLine(
    $"{ languages[0],-20 }\t{ languages[languages.Length-1],-20 }");
System.Console.WriteLine(
    $"After clearing, the array size is: { languages.Length }");
}
```

The results of Listing 2.51 are shown in Output 2.20.

## OUTPUT 2.20

```
The wave of the future, COBOL, is at index 2.

First Element        Last Element
---------------      -------------
C#                    Visual Basic
Visual Basic          C#

After clearing, the array size is: 9
```

Access to these methods is obtained through the System.Array class. For the most part, using these methods is self-explanatory, except for two noteworthy items:

- Before using the BinarySearch() method, it is important to sort the array. If values are not sorted in increasing order, the incorrect index may be returned. If the search element does not exist, the value returned is negative. (Using the complement operator, ~index, returns the first index, if any, that is larger than the searched value.)
- The Clear() method does not remove elements of the array and does not set the length to zero. The array size is fixed and cannot be modified. Therefore, the Clear() method sets each element in the array to its default value (false, 0, or null). This explains why Console.WriteLine() creates a blank line when writing out the array after Clear() is called.

## Language Contrast: Visual Basic—Redimensioning Arrays

Visual Basic includes a Redim statement for changing the number of items in an array. Although there is no equivalent C#-specific keyword, there is a method available in .NET 2.0 that will re-create the array and then copy all the elements over to the new array. This method is called System.Array.Resize.

## Array Instance Methods

Like strings, arrays have instance members that are accessed not from the data type, but directly from the variable. Length is an example of an instance member because access to Length is through the array variable, not the class. Other significant instance members are GetLength(), Rank, and Clone().

Retrieving the length of a particular dimension does not require the Length property. To retrieve the size of a particular rank, an array includes a GetLength() instance method. When calling this method, it is necessary to specify the rank whose length will be returned (see Listing 2.52).

## LISTING 2.52: Retrieving a Particular Dimension's Size

```
bool[,] cells;
cells = new bool[2,3,3];
System.Console.WriteLine(cells.GetLength(0));  // Displays 2
```

The results of Listing 2.52 appear in Output 2.21.

## OUTPUT 2.21

```
2
```

Listing 2.52 displays 2 because that is the number of elements in the first dimension.

It is also possible to retrieve the entire array’s rank by accessing the array’s Rank member. cells.Rank, for example, will return 3.

By default, assigning one array variable to another copies only the array reference, not the individual elements of the array. To make an entirely new copy of the array, use the array’s Clone() method. The Clone() method will return a copy of the array; changing any of the members of this new array will not affect the members of the original array.

## Strings As Arrays

Variables of type string are accessible like an array of characters. For example, to retrieve the fourth character of a string called palindrome you can call palindrome[3]. Note, however, that because strings are immutable, it is not possible to assign particular characters within a string. C#, therefore, would not allow palindrome[3]='a', where palindrome is declared as a string. Listing 2.53 uses the array accessor to determine whether an argument on the command line is an option, where an option is identified by a dash as the first character.

## LISTING 2.53: Looking for Command-Line Options

```
string[] args;
...
if(args[0][0] == '-')
{
    //This parameter is an option
}
```

This snippet uses the if statement, which is covered in Chapter 3. In addition, it presents an interesting example because you use the array accessor to retrieve the first element in the array of strings, args. Following the first array accessor is a second one, which retrieves the first character of the string. The code, therefore, is equivalent to that shown in Listing 2.54.
