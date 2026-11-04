```
public static bool operator false(param-type operand)
{
    // return true or false
}
```

Notice that each returns a bool result.

The following example shows how true and false can be implemented for the ThreeD class. Each assumes that a ThreeD object is true if at least one coordinate is non-zero. If all three coordinates are zero, then the object is false. The decrement operator is also implemented for the purpose of illustration.

```
// Overload true and false for ThreeD.

using System;

// A three-dimensional coordinate class.
class ThreeD {
    int x, y, z; // 3-D coordinates
    public ThreeD() { x = y = z = 0; }
    public ThreeD(int i, int j, int k) { x = i; y = j; z = k; }

    // Overload true.
    public static bool operator true(ThreeD op) {
        if((op.x != 0) || (op.y != 0) || (op.z != 0))
            return true; // at least one coordinate is non-zero
        else
            return false;
    }

    // Overload false.
    public static bool operator false(ThreeD op) {
        if((op.x == 0) && (op.y == 0) && (op.z == 0))
            return true; // all coordinates are zero
        else
            return false;
    }

    // Overload unary --.
    public static ThreeD operator --(ThreeD op)
    {
        ThreeD result = new ThreeD();

        // Return the decremented result.
        result.x = op.x - 1;
        result.y = op.y - 1;
        result.z = op.z - 1;

        return result;
    }

    // Show X, Y, Z coordinates.
    public void Show()
    {
```