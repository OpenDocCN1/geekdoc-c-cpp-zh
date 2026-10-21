# Program 8.7 | CONCEPT OF VARIABLE ARGUMENTS

```
using System;
class Params
{
    static void Parray ( params int [] arr )
    {
        Console.Write("Array elements are:");
        foreach (int i in arr)
            Console.Write(" " + i);
        Console.WriteLine();
    }
    public static void Main()
    {
        int [] x = { 11, 22, 33 };
        Parray ( x );      // call 1
        Parray ( );        // call 2
        Parray ( 100, 200 );   // call 3
    }
}
```

The output of Program 8.7 would be:
Array elements are : 11 22 33
Array elements are :
Array elements are : 100 200

Note that the invocations Parray ( ); and Parray ( 100, 200 ); are equivalent to:
Parray ( new int [] { } );
Parray ( new int [] { 100, 200 } );

We can also use parameter arrays of type object. Example:

```
public static void Main()
{
    Oarray ( 10, 20, "abc" );
}
static void Oarray ( params object [] x )
{
    foreach ( object i in x )
    {
        Console.WriteLine( i );
    }
}
```

The method Oarray is passed for an array of object references. The method call automatically builds an object array to hold the arguments, boxing value types as necessary.

Note that while it is permitted to use parameter arrays along with the value parameters, it is not allowed to combine the params modifier with the ref and out modifiers.

Program 8.8 uses the concept of variable number of parameters being passed to a single method. This program calculates the average of any set of numbers passed as parameters to the method avgVal().