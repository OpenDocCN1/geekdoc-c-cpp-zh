that we want people using your Vector to be able to write double X = a*b to calculate the inner product of two Vector objects (a and b). The relevant overload looks like this:

```
public static double operator * (Vector lhs, Vector rhs)
{
    return lhs.x * rhs.x + lhs.y * rhs.y + lhs.z * rhs.z;
}
```

Now that you understand the arithmetic operators, you can check that they work using a simple test method:

```
static void Main()
{
    // stuff to demonstrate arithmetic operations
    Vector vect1, vect3;
    vect1 = new Vector(1.0, 1.5, 2.0);
    vect2 = new Vector(0.0, 0.0, -10.0);

    vect3 = vect1 + vect2;

    Console.WriteLine("vect1 = " + vect1);
    Console.WriteLine("vect2 = " + vect2);
    Console.WriteLine("vect3 = vect1 + vect2 = " + vect3);
    Console.WriteLine("2*vect3 = " + 2*vect3);
    vect3 += vect2;

    Console.WriteLine("vect3+=vect2 gives " + vect3);

    vect3 = vect1*2;

    Console.WriteLine("Setting vect3=vect1*2 gives " + vect3);

    double dot = vect1*vect3;

    Console.WriteLine("vect1*vect3 = " + dot);
}
```

Running this code (Vectors2.cs) produces the following result:

# VECTORS2

```
vect1 = { 1, 1.5, 2 }
vect2 = { 0, 0, -10 }
vect3 = vect1 + vect2 = { 1, 1.5, -8 }
2*vect3 = { 2, 3, -16 }
vect3+=vect2 gives { 1, 1.5, -18 }
Setting vect3=vect1*2 gives { 2, 3, 4 }
vect1*vect3 = 14.5
```

This shows that the operator overloads have given the correct results, but if you look at the test code closely, you might be surprised to notice that it actually used an operator that wasn't overloaded — the addition assignment operator, +=

```
vect3 += vect2;

Console.WriteLine("vect3 += vect2 gives " + vect3);
```

Although += normally counts as a single operator, it can be broken down into two steps: the addition and the assignment. Unlike the C++ language, C# will not actually allow you to overload the = operator, but if you overload +, the compiler will automatically use your overload of + to work out how to perform a += operation. The same principle works for all the assignment operators such as -=, *=, /=, &=, and so on.