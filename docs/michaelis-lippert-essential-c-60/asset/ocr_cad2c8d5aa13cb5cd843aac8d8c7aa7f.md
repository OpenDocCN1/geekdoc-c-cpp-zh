```
public static readonly Guid ComIUnknownGuid =
    new Guid("00000000-0000-0000-C000-000000000046");
```

The same, however, is not possible using a constant because of the fact that there is no C# literal representation of a Guid.

Given the guideline that fields should not be accessed from outside their wrapping property, those programming in a C# 6.0 world will discover that that there is almost never a need to use the readonly modifier. Instead, it is preferable to use a read-only automatically implemented property, as discussed earlier in the chapter.

Consider Listing 5.44 for one more read-only example.

# LISTING 5.44: Declaring a Read-Only Automatically Implemented Property

```
class TicTacToeBoard
{
    // Set both player's move to all false (blank).
    //    | |
    // --+---+--
    //    | |
    // --+---+--
    //    | |
    public bool[,] Cells { get; } = new bool[2, 3, 3];
    // Error: The property Cells cannot
    // be assigned to because it is read-only
    public void SetCells(bool[,] value) =>
        Cells = new bool[2, 3, 3];

    // ...
}
```

Whether implemented using C# 6.0 read-only automatically implemented properties or the readonly modifier on a field, providing for immutability of the array reference is a useful defensive coding technique. It ensures that the array instance remains the same, while allowing the elements within the array to change. Without the read-only constraint, it would be all too easy to mistakenly assign a new array to the member, thereby discarding the existing array rather than updating individual array elements. In other words, using a read-only approach with an array does not freeze the contents of the array. Rather, it freezes the array instance (and therefore the number of elements in the array) because it is not possible to reassign the value to a new instance. The elements of the array are still writeable.