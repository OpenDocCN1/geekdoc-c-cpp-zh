//Add the contents of u1 and u2
//to the new Vector object
//Return the new vector object

Program 15.2 illustrates how this is accomplished. This program overloads the binary plus operator to add two complex numbers of type:
 x = a + jb

# Program 15.2 OVERLOADING + OPERATOR

```
using System;
class Complex
{
    double x;          //real part
    double y;          //imaginary part
    public Complex ()
    {
    }
    public Complex(double real, double imag)
    {
        x = real;
        y = imag;
    }
    public static Complex operator + (Complex c1, Complex c2)
    {
        Complex c3 = new Complex ();
        c3.x = c1.x + c2.x;
        c3.y = c1.y + c2.y;
        return (c3);
    }
    public void Display()
    {
        Console.Write(x);
        Console.Write(" + j" + y);
        Console.WriteLine();
    }
}
class ComplexTest
{
    public static void Main()
    {
        Complex a, b, c;
        a = new Complex (2.5 , 3.5);
        b = new Complex (1.6, 2.7);
        c = a + b;
        Console.Write(" a = ");
        a.Display();
        Console.Write("b = ");
        b.Display();
```