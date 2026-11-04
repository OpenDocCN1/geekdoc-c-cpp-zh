
Here, a new object is created that contains the negated fields of the operand. This object is then returned. Notice that the operand is unchanged. Again, this is in keeping with the usual meaning of the unary minus. For example, in an expression such as this,

a = -b

a receives the negation of b, but b is not changed.

In C#, overloading ++ and -- is quite easy; simply return the incremented or decremented value, but don't change the invoking object. C# will automatically handle that for you, taking into account the difference between the prefix and postfix forms. For example, here is an operator++() method for the ThreeD class:

```csharp
// Overload unary ++.
public static ThreeD operator ++(ThreeD op)
{
    ThreeD result = new ThreeD();

    // Return the incremented result.
    result.x = op.x + 1;
    result.y = op.y + 1;
    result.z = op.z + 1;

    return result;
}
```

Here is an expanded version of the previous example program that demonstrates the unary – and the ++ operator:

```csharp
// More operator overloading.
using System;

// A three-dimensional coordinate class.
class ThreeD {
    int x, y, z; // 3-D coordinates

    public ThreeD() { x = y = z = 0; }
    public ThreeD(int i, int j, int k) { x = i; y = j; z = k; }

    // Overload binary +.
    public static ThreeD operator +(ThreeD op1, ThreeD op2)
    {
        ThreeD result = new ThreeD();

        /* This adds together the coordinates of the two points
           and returns the result. */
        result.x = op1.x + op2.x;
        result.y = op1.y + op2.y;
        result.z = op1.z + op2.z;

        return result;
    }

    // Overload binary -.
```

```csharp
Console.Write("Here is b: ");
b.Show();
Console.WriteLine();

c = a + b; // add a and b together
Console.Write("Result of a + b: ");
c.Show();
Console.WriteLine();

c = a + b + c; // add a, b, and c together
Console.Write("Result of a + b + c: ");
c.Show();
Console.WriteLine();

c = c - a; // subtract a
Console.Write("Result of c - a: ");
c.Show();
Console.WriteLine();

c = c - b; // subtract b
Console.Write("Result of c - b: ");
c.Show();
Console.WriteLine();

c = -a; // assign -a to c
Console.Write("Result of -a: ");
c.Show();
Console.WriteLine();

c = a++; // post-increment a
Console.WriteLine("Given c = a++");
Console.Write("c is ");
c.Show();
Console.WriteLine("a is ");
a.Show();

// Reset a to 1, 2, 3
a = new ThreeD(1, 2, 3);
Console.Write("\nResetting a to ");
a.Show();

c = ++a; // pre-increment a
Console.WriteLine("\nGiven c = ++a");
Console.Write("c is ");
c.Show();
Console.WriteLine("a is ");
a.Show();
}
}
```

The output from the program is shown here:

```
Here is a: 1, 2, 3
Here is b: 10, 10, 10

Result of a + b: 11, 12, 13

Result of a + b + c: 22, 24, 26

Result of c - a: 21, 22, 23

Result of c - b: 11, 12, 13

Result of -a: -1, -2, -3

Given c = a++
c is 1, 2, 3
a is 2, 3, 4

Resetting a to 1, 2, 3

Given c = ++a
c is 2, 3, 4
a is 2, 3, 4
```

## Handling Operations on C# Built-in Types

For any given class and operator, an operator method can, itself, be overloaded. One of the most common reasons for this is to allow operations between a class type and other types of data, such as a built-in type. For example, once again consider the ThreeD class. To this point, you have seen how to overload the + so that it adds the coordinates of one ThreeD object to another. However, this is not the only way in which you might want to define addition for ThreeD. For example, it might be useful to add an integer value to each coordinate of a ThreeD object. Such an operation could be used to translate axes. To perform such an operation, you will need to overload + a second time, as shown here:

```csharp
// Overload binary + for ThreeD + int.
public static ThreeD operator +(ThreeD op1, int op2)
{
    ThreeD result = new ThreeD();

    result.x = op1.x + op2;
    result.y = op1.y + op2;
    result.z = op1.z + op2;

    return result;
}
```

Notice that the second parameter is of type int. Thus, the preceding method allows an integer value to be added to each field of a ThreeD object. This is permissible because, as explained earlier, when overloading a binary operator, one of the operands must be of the same type as the class for which the operator is being overloaded. However, the other operand can be of any other type.

Here is a version of ThreeD that has two overloaded + methods:

```csharp
// Overload addition for ThreeD + ThreeD, and for ThreeD + int.
using System;
// A three-dimensional coordinate class.
class ThreeD {
    int x, y, z; // 3-D coordinates
    public ThreeD() { x = y = z = 0; }
    public ThreeD(int i, int j, int k) { x = i; y = j; z = k; }
    // Overload binary + for ThreeD + ThreeD.
    public static ThreeD operator +(ThreeD op1, ThreeD op2)
    {
        ThreeD result = new ThreeD();
        /* This adds together the coordinates of the two points
           and returns the result. */
        result.x = op1.x + op2.x;
        result.y = op1.y + op2.y;
        result.z = op1.z + op2.z;
        return result;
    }
    // Overload binary + for object + int.
    public static ThreeD operator +(ThreeD op1, int op2)
    {
        ThreeD result = new ThreeD();
        result.x = op1.x + op2;
        result.y = op1.y + op2;
        result.z = op1.z + op2;
        return result;
    }
    // Show X, Y, Z coordinates.
    public void Show()
    {
        Console.WriteLine(x + ", " + y + ", " + z);
    }
}
class ThreeDDemo {
    static void Main() {
        ThreeD a = new ThreeD(1, 2, 3);
        ThreeD b = new ThreeD(10, 10, 10);
        ThreeD c = new ThreeD();
        Console.Write("Here is a: ");
        a.Show();
        Console.WriteLine();
        Console.Write("Here is b: ");
    }
}
```

```csharp
b.Show();
Console.WriteLine();

c = a + b; // ThreeD + ThreeD
Console.Write("Result of a + b: ");
c.Show();
Console.WriteLine();

c = b + 10; // ThreeD + int
Console.Write("Result of b + 10: ");
c.Show();
}
```

The output from this program is shown here:

```
Here is a: 1, 2, 3

Here is b: 10, 10, 10

Result of a + b: 11, 12, 13

Result of b + 10: 20, 20, 20
```

As the output confirms, when the + is applied to two ThreeD objects, their coordinates are added together. When the + is applied to a ThreeD object and an integer, the coordinates are increased by the integer value.

While the overloading of + just shown certainly adds a useful capability to the ThreeD class, it does not quite finish the job. Here is why. The operator+(ThreeD, int) method allows statements like this:

```
ob1 = ob2 + 10;
```

It does not, unfortunately, allow ones like this:

```
ob1 = 10 + ob2;
```

The reason is that the integer argument is the second argument, which is the right-hand operand, but the preceding statement puts the integer argument on the left. To allow both forms of statements, you will need to overload the + yet another time. This version must have its first parameter as type int and its second parameter as type ThreeD. One version of the operator+( ) method handles ThreeD + integer, and the other handles integer + ThreeD. Overloading the + (or any other binary operator) this way allows a built-in type to occur on the left or right side of the operator. Here is a version ThreeD that overloads the + operator as just described:

```csharp
// Overload the + for ThreeD + ThreeD, ThreeD + int, and int + ThreeD.

using System;

// A three-dimensional coordinate class.
class ThreeD {
    int x, y, z; // 3-D coordinates
```

```csharp
public ThreeD() { x = y = z = 0; }
public ThreeD(int i, int j, int k) { x = i; y = j; z = k; }

// Overload binary + for ThreeD + ThreeD.
public static ThreeD operator +(ThreeD op1, ThreeD op2)
{
    ThreeD result = new ThreeD();

    /* This adds together the coordinates of the two points
       and returns the result. */
    result.x = op1.x + op2.x;
    result.y = op1.y + op2.y;
    result.z = op1.z + op2.z;

    return result;
}

// Overload binary + for ThreeD + int.
public static ThreeD operator +(ThreeD op1, int op2)
{
    ThreeD result = new ThreeD();

    result.x = op1.x + op2;
    result.y = op1.y + op2;
    result.z = op1.z + op2;

    return result;
}

// Overload binary + for int + ThreeD.
public static ThreeD operator +(int op1, ThreeD op2)
{
    ThreeD result = new ThreeD();

    result.x = op2.x + op1;
    result.y = op2.y + op1;
    result.z = op2.z + op1;

    return result;
}

// Show X, Y, Z coordinates.
public void Show()
{
    Console.WriteLine(x + ", " + y + ", " + z);
}

class ThreeDDemo {
    static void Main() {
        ThreeD a = new ThreeD(1, 2, 3);
        ThreeD b = new ThreeD(10, 10, 10);
        ThreeD c = new ThreeD();
```
