Unlike constant fields, readonly-decorated fields can vary from one instance to the next. In fact, a read-only field’s value can change within the constructor. Furthermore, read-only fields occur as either instance or static fields. Another key distinction is that you can assign the value of a read-only field at execution time rather than just at compile time. Given that read-only fields must be set in the constructor or initializer, such fields are the one case where the compiler requires the fields be accessed from code outside their corresponding property. Besides this one exception, you should avoid accessing a backing field from anywhere other than its wrapping property.

Another important feature of readonly-decorated fields over const fields is that read-only fields are not limited to types with literal values. It is possible, for example, to declare a readonly System.Guid instance field:

```
public static readonly Guid ComIUnknownGuid =
    new Guid("00000000-0000-0000-C000-000000000046");
```

The same, however, is not possible using a constant because of the fact that there is no C# literal representation of a GUID.

Given the guideline that fields should not be accessed from outside their wrapping property, those programming in a C# 6.0 (or later) world will discover that that there is almost never a need to use the readonly modifier. Instead, it is preferable to use a read-only automatically implemented property, as discussed earlier in the chapter.

Consider Listing 6.45 for one more read-only example.

# **LISTING 6.45: Declaring a Read-Only Automatically Implemented Property**

```
class TicTacToeBoard
{
    // Set both players' moves to all false (blank)
    //  |   |
    //  |---|
    //  |   |
    //  |---|
    //  |   |
    public bool[,,] Cells { get; } = new bool[2, 3, 3];
    // Error: The property Cells cannot
    // be assigned to because it is read-only
    //public void SetCells(bool[,,] value) =>
        Cells = new bool[2, 3, 3];
    // ...
}
```