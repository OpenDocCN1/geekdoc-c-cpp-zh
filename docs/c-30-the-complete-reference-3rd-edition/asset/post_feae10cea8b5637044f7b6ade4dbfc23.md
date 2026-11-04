
Although you cannot overload the cast operator ( ) explicitly, you can create conversion operators, as shown earlier, that perform this function.

It may seem like a serious restriction that operators such as += can’t be overloaded, but it isn’t. In general, if you have defined an operator, then if that operator is used in a compound assignment, your overloaded operator method is invoked. Thus, += automatically uses your version of operator+( ). For example, assuming the ThreeD class, if you use a sequence like this

```
ThreeD a = new ThreeD(1, 2, 3);
ThreeD b = new ThreeD(10, 10, 10);

b += a; // add a and b together
```

ThreeD’s operator+( ) is automatically invoked, and b will contain the coordinate 11, 12, 13.

One last point: Although you cannot overload the [ ] array indexing operator using an operator method, you can create indexers, which are described in the next chapter.

## Another Example of Operator Overloading

Throughout this chapter we have been using the ThreeD class to demonstrate operator overloading, and in this regard it has served us well. Before concluding this chapter, however, it is useful to work through another example. Although the general principles of operator overloading are the same no matter what class is used, the following example helps show the power of operator overloading—especially where type extensibility is concerned.

This example develops a four-bit integer type and defines several operations for it. As you might know, in the early days of computing, the four-bit quantity was common because it represented half a byte. It is also large enough to hold one hexadecimal digit. Since four bits are half a byte, a four-bit quantity is sometimes referred to as a nybble. In the days of front-panel machines in which programmers entered code one nybble at a time, thinking in terms of nybbles was an everyday affair! Although not as common now, a four-bit type still makes an interesting addition to the other C# integers. Traditionally, a nybble is an unsigned value.

The following example uses the Nybble class to implement a nybble data type. It uses an int for its underlying storage, but it restricts the values that can be held to 0 through 15. It defines the following operators:

- Addition of a Nybble to a Nybble
- Addition of an int to a Nybble
- Addition of a Nybble to an int
- Greater than and less than
- The increment operator
- Conversion to Nybble from int
- Conversion to int from Nybble

These operations are sufficient to show how a class type can be fully integrated into the C# type system. However, for complete Nybble implementation, you will need to define all of the other operators. You might want to try adding others on your own.

The complete Nybble class is shown here along with a NybbleDemo, which demonstrates its use:

```
// Create a 4-bit type called Nybble.
using System;

// A 4-bit type.
class Nybble {
    int val; // underlying storage

    public Nybble() { val = 0; }

    public Nybble(int i) {
        val = i;
        val = val & 0xF; // retain lower 4 bits
    }

    // Overload binary + for Nybble + Nybble.
    public static Nybble operator +(Nybble op1, Nybble op2)
    {
        Nybble result = new Nybble();

        result.val = op1.val + op2.val;

        result.val = result.val & 0xF; // retain lower 4 bits

        return result;
    }

    // Overload binary + for Nybble + int.
    public static Nybble operator +(Nybble op1, int op2)
    {
        Nybble result = new Nybble();

        result.val = op1.val + op2;

        result.val = result.val & 0xF; // retain lower 4 bits

        return result;
    }

    // Overload binary + for int + Nybble.
    public static Nybble operator +(int op1, Nybble op2)
    {
        Nybble result = new Nybble();

        result.val = op1 + op2.val;

        result.val = result.val & 0xF; // retain lower 4 bits

        return result;
    }

    // Overload ++.
    public static Nybble operator ++(Nybble op)
    {
        Nybble result = new Nybble();
        result.val = op.val + 1;

        result.val = result.val & 0xF; // retain lower 4 bits

        return result;
    }

    // Overload >.
    public static bool operator >(Nybble op1, Nybble op2)
    {
        if(op1.val > op2.val) return true;
        else return false;
    }

    // Overload <.
    public static bool operator <(Nybble op1, Nybble op2)
    {
        if(op1.val < op2.val) return true;
        else return false;
    }

    // Convert a Nybble into an int.
    public static implicit operator int (Nybble op)
    {
        return op.val;
    }

    // Convert an int into a Nybble.
    public static implicit operator Nybble (int op)
    {
        return new Nybble(op);
    }
}

class NybbleDemo {
    static void Main() {
        Nybble a = new Nybble(1);
        Nybble b = new Nybble(10);
        Nybble c = new Nybble();
        int t;

        Console.WriteLine("a: " + (int) a);
        Console.WriteLine("b: " + (int) b);

        // Use a Nybble in an if statement.
        if(a < b) Console.WriteLine("a is less than b\n");

        // Add two Nybbles together.
        c = a + b;
        Console.WriteLine("c after c = a + b: " + (int) c);

        // Add an int to a Nybble.
        a += 5;
        Console.WriteLine("a after a += 5: " + (int) a);

        Console.WriteLine();

        // Use a Nybble in an int expression.
        t = a * 2 + 3;
        Console.WriteLine("Result of a * 2 + 3: " + t);

        Console.WriteLine();

        // Illustrate int assignment and overflow.
        a = 19;
        Console.WriteLine("Result of a = 19: " + (int) a);

        Console.WriteLine();

        // Use a Nybble to control a loop.
        Console.WriteLine("Control a for loop with a Nybble.");
        for(a = 0; a < 10; a++)
            Console.WriteLine(a + " ");

        Console.WriteLine();
    }
}
```

The output from the program is shown here:

```
a: 1
b: 10
a is less than b

c after c = a + b: 11
a after a += 5: 6

Result of a * 2 + 3: 15

Result of a = 19: 3

Control a for loop with a Nybble.
0 1 2 3 4 5 6 7 8 9
```

Although most of the operation of Nybble should be easy to understand, there is one important point to make: The conversion operators play a large role in the integration of Nybble into the C# type system. Because conversions are defined from Nybble to int and from int to Nybble, a Nybble object can be freely mixed in arithmetic expressions. For example, consider this expression from the program:

```
t = a * 2 + 3;
```

Here, t is an int, as are 2 and 3, but a is a Nybble. These two types are compatible in the expression because of the implicit conversion of Nybble to int. In this case, since the rest of the expression is of type int, a is converted to int by its conversion method.

The conversion from int to Nybble allows a Nybble object to be assigned an int value. For example, in the program, the statement

```
a = 19;
```

works like this. The conversion operator from int to Nybble is executed. This causes a new Nybble object to be created that contains the low-order 4 bits of the value 19 (which is 3 because 19 overflows the range of a Nybble). This object is then assigned to a. Without the conversion operators, such expressions would not be allowed.

The conversion of Nybble to int is also used by the for loop. Without this conversion, it would not be possible to write the for loop in such a straightforward way.

## Indexers and Properties

This chapter examines two special types of class members that have a close relationship to each other: indexers and properties. Each expands the power of a class by enhancing its integration into C#’s type system and improving its resiliency. Indexers provide the mechanism by which an object can be indexed like an array. Properties offer a streamlined way to manage access to a class’ instance data. They relate to each other because both rely upon another feature of C#: the accessor.

### Indexers

As you know, array indexing is performed using the [] operator. It is possible to define the [] operator for classes that you create, but you don’t use an operator method. Instead, you create an indexer. An indexer allows an object to be indexed like an array. The main use of indexers is to support the creation of specialized arrays that are subject to one or more constraints. However, you can use an indexer for any purpose for which an array-like syntax is beneficial. Indexers can have one or more dimensions. We will begin with one-dimensional indexers.

### Creating One-Dimensional Indexers

A one-dimensional indexer has this general form:

```
element-type this[int index] {
    // The get accessor
    get {
        // return the value specified by index
    }

    // The set accessor
    set {
        // set the value specified by index
    }
}
```
