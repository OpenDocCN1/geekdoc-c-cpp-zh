```
z = c;
}
public void Display ()
{
    Console.Write(" " + x);
    Console.Write(" " + y);
    Console.Write(" " + z);
    Console.WriteLine();
}
public static Space operator - (Space s)
{
    s.x = -s.x;
    s.y = -s.y;
    s.z = -s.z;
}
}
class SpaceTest
{
    public static void Main()
    {
        Space s = new Space ( 10, -20, 30 );
        Console.Write(" s : ");
        s.Display();
        -s;            //activates opeator -() method
        Console.Write(" s : ");
        s.Display();
    }
}
```

Program 15.1 will produce the following output:
S : 10 -20 30
S : -10 20 -30

# 15.6 OVERLOADING BINARY OPERATORS

We have just seen how to overload a unary operator. The same mechanism can be used to overload a binary operator. We can always use methods to add two objects. A statement like
C = sum ( A, B); //functional notation
is possible. The functional notation can be replaced by a natural looking expression
C = A + B; //arithmetic notation.
by overloading the + operator using an operator + () method. Here is the syntax used to define the operator + () method.

```
public static Vector operator + (Vector u1, Vector u2)
{
    //Create a new Vector object
```