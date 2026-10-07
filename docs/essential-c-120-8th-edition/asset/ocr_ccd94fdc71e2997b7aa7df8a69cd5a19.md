# 130 Chapter 3: More with Data Types

LISTING 3.28: Retrieving a Particular Dimension's Size

```
bool[,] cells;
cells = new bool[2, 3, 3];
Console.WriteLine(cells.GetLength(0)); // Displays 2
Console.WriteLine(cells.Rank); // Displays 3
```

OUTPUT 3.3

2

Listing 3.28 displays 2 because that is the number of elements in the first dimension.

It is also possible to retrieve the entire array's rank by accessing the array's rank member. cells.Rank, for example, returns 3 (see Listing 3.28).

By default, assigning one array variable to another copies only the array reference, not the individual elements of the array. To make an entirely new copy of the array, use the array's Clone() method. The Clone() method returns a copy of the array; changing any of the members of this new array does not affect the members of the original array.

# Strings as Arrays

Variables of type string are accessible like an array of characters. For example, retrieve the fourth character of a string called palindrome, you can call palindrome[3]. Note, however, because strings are immutable, it is not possible to assign particular characters within a string. C#, therefore, would not allow palindrome[3]='a', where palindrome is declared as a string. Listing 3.29 uses the array accessor to determine whether an argument on the command line is identified by a dash as the first character.

LISTING 3.29: Looking for Command-Line Options

```
public static void Main(string[] args)
{
  // ...
  if(args[0][0] == '-')
  {
    // This parameter is an option
```