the return type is also a Vector. For this particular override of the addition operator, the return type is the same as the containing class, but that is not necessarily the case, as you see later in this example. The two parameters are the things you are operating on. For binary operators (those that take two parameters), such as the addition and subtraction operators, the first parameter is the value on the left of the operator, and the second parameter is the value on the right.

The implementation of this operator returns a new Vector that is initialized using X, Y, and Z properties from the left and right variables.

C# requires that all operator overloads be declared as public and static, which means they are associated with their class or struct, not with a particular instance. Because of this, the body of the operator overload has no access to non-static class members or the this identifier. This is fine because the parameters provide all the input data the operator needs to know to perform its task.

Now all you need to do is write some simple code to test the Vector struct (code file OperatorOverloadingSample/Program.cs):

```
static void Main()
{
    Vector vect1, vect2, vect3;

    vect1 = new Vector(3.0, 3.0, 1.0);
    vect2 = new Vector(2.0, -4.0, -4.0);
    vect3 = vect1 + vect2;

    WriteLine($"vect1 = {vect1}");
    WriteLine($"vect2 = {vect2}");
    WriteLine($"vect3 = {vect3}");
}
```

Compiling and running this code returns the following result:

```
vect1 = ( 3, 3, 1 )
vect2 = ( 2, -4, -4 )
vect3 = ( 5, -1, -3 )
```

In addition to adding vectors, you can multiply and subtract them and compare their values. In this section, you develop the Vector example further by adding a few more operator overloads. You won’t develop the complete set that you’d probably need for a fully functional Vector type, but you develop enough to demonstrate some other aspects of operator overloading. First, you overload the multiplication operator to support multiplying vectors by a scalar and multiplying vectors by another vector.

Multiplying a vector by a scalar simply means multiplying each component individually by the scalar: for example, 2 * (1.0, 2.5, 2.0) returns (2.0, 5.0, 4.0). The relevant operator overload looks similar to this (code file OperatorOverloadingSample2/Vector.cs):

```
public static Vector operator *(double left, Vector right) =>
    new Vector(left * right.X, left * right.Y, left * right.Z);
```