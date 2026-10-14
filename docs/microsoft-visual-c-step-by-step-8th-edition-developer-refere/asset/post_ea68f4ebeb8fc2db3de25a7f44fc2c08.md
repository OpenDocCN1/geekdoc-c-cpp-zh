
```
class Complex
{
    ...
    public static Complex operator *(Complex lhs, Complex rhs)
    {
        return new Complex(lhs.Real * rhs.Real - lhs.Imaginary * rhs.Imaginary,
            lhs.Imaginary * rhs.Real + lhs.Real * rhs.Imaginary);
    }

    public static Complex operator /(Complex lhs, Complex rhs)
    {
        int realElement = (lhs.Real * rhs.Real + lhs.Imaginary * rhs.Imaginary) /
            (rhs.Real * rhs.Real + rhs.Imaginary * rhs.Imaginary);

        int imaginaryElement = (lhs.Imaginary * rhs.Real - lhs.Real * rhs.Imaginary) /
            (rhs.Real * rhs.Real + rhs.Imaginary * rhs.Imaginary);

        return new Complex(realElement, imaginaryElement);
    }
}
```

These operators follow the same form as the previous two operators, although the calculations are a little more complicated. (The calculation for the / operator has been broken down into two steps to avoid lengthy lines of code.)

10. Display the Program.cs file in the Code and Text Editor window. Add the following statements shown in bold to the doWork method of the Program class and delete the // TODO: comment:

Click here to view code image

```
static void doWork()
{
    Complex first = new Complex(10, 4);
    Complex second = new Complex(5, 2);

    Console.WriteLine($"first is {first}");
    Console.WriteLine($"second is {second}");

    Complex temp = first + second;
    Console.WriteLine($"Add: result is {temp}");

    temp = first - second;
    Console.WriteLine($"Subtract: result is {temp}");

    temp = first * second;
    Console.WriteLine($"Multiply: result is {temp}");
```

```
temp = first / second;
Console.WriteLine($"Divide: result is {temp}");
}
```

This code creates two Complex objects that represent the complex values (10 + 4i) and (5 + 2i). The code displays them and then tests each of the operators you have just defined, displaying the results in each case.

11. On the Debug menu, click Start Without Debugging.

Verify that the application displays the results shown in the following image:

![](img/16f6e3fe08f01ddadb2741a92c392b0e_591_0.png)

12. Close the application, and return to the Visual Studio 2015 programming environment.

You have now created a type that models complex numbers and supports basic arithmetic operations. In the next exercise, you will extend the Complex class and provide the equality operators, == and !=.

## Implement the equality operators

+   1. In Visual Studio 2015, display the Complex.cs file in the Code and Text Editor window.
+   2. Add the == and != operators to the Complex class as shown in bold in the following example.

Click here to view code image

```
class Complex
{
    ...
    public static bool operator ==(Complex lhs, Complex rhs)
    {
        return lhs.Equals(rhs);
    }

    public static bool operator !=(Complex lhs, Complex rhs)
    {
        return !(lhs.Equals(rhs));
    }
}
```

Notice that both of these operators make use of the Equals method. The Equals method compares an instance of a class against another instance

specified as an argument. It returns *true* if they have equivalent values and *false* otherwise.

3. On the Build menu, click Rebuild Solution.

The Error List window displays the following warning messages:

Click here to view code image

```
'ComplexNumbers.Complex' defines operator == or operator != but does not override
Object.Equals(object o)
'ComplexNumbers.Complex' defines operator == or operator != but does not override
Object.GetHashCode()
```

If you define the != and == operators, you should also override the *Equals* and *GetHashCode* methods inherited from *System.Object*.

# Note

If the Error List window is not visible, click Error List on the View menu.

4. Override the *Equals* method in the *Complex* class, as shown here in bold:

Click here to view code image

```
class Complex
{
    ...
    public override bool Equals(Object obj)
    {
        if (obj is Complex)
        {
            Complex compare = (Complex)obj;
            return (this.Real == compare.Real) &&
                   (this.Imaginary == compare.Imaginary);
        }
        else
        {
            return false;
        }
    }
}
```

The *Equals* method takes an *Object* as a parameter. This code verifies that the type of the parameter is actually a *Complex* object. If it is, this code compares the values in the *Real* and *Imaginary* properties in the current instance and the parameter passed in. If they are the same, the method returns *true*; otherwise, it returns *false*. If the parameter passed in is not a *Complex* object, the method returns *false*.

## Important

It is tempting to write the Equals method like this:

Click here to view code image

```
public override bool Equals(Object obj)
{
    Complex compare = obj as Complex;
    if (compare != null)
    {
        return (this.Real == compare.Real) &&
            (this.Imaginary == compare.Imaginary);
    }
    else
    {
        return false;
    }
}
```

However, the expression compare != null invokes the != operator of the Complex class, which calls the Equals method again, resulting in a recursive loop.

5. Override the GetHashCode method. This implementation simply calls the method inherited from the Object class, but you can provide your own mechanism to generate a hash code for an object if you prefer.

Click here to view code image

```
Class Complex
{
    ...
    public override int GetHashCode()
    {
        return base.GetHashCode();
    }
}
```

6. On the Build menu, click Rebuild Solution.

Verify that the solution now builds without reporting any warnings.

7. Display the Program.cs file in the Code and Text Editor window. Add the following code shown in bold to the end of the doWork method:

Click here to view code image

```
static void doWork()
{
    ...
    if (temp == first)
    {
        Console.WriteLine("Comparison: temp == first");
```

```
}
else
{
    Console.WriteLine("Comparison: temp != first");
}

if (temp == temp)
{
    Console.WriteLine("Comparison: temp == temp");
}
else
{
    Console.WriteLine("Comparison: temp != temp");
}
}
```

# Note

The expression temp == temp generates the warning message “Comparison made to same variable; did you mean to compare to something else?” In this case, you can ignore the warning because this comparison is intentional; it is to verify that the == operator is working as expected.

8. On the Debug menu, click Start Without Debugging. Verify that the final two messages displayed are these:

```
Comparison: temp != first
Comparison: temp == temp
```

9. Close the application, and return to Visual Studio 2015.

## Understanding conversion operators

Sometimes, you need to convert an expression of one type to another. For example, the following method is declared with a single double parameter:

Click here to view code image

```
class Example
{
    public static void MyDoubleMethod(double parameter)
    {
        ...
    }
}
```

You might reasonably expect that only values of type double could be used as arguments when your code calls MyDoubleMethod, but this is not so. The C# compiler also allows MyDoubleMethod to be called with an argument of some

other type, but only if the value of the argument can be converted to a double. For example, if you provide an int argument, the compiler generates code that converts the value of the argument to a double when the method is called.

## Providing built-in conversions

The built-in types have some built-in conversions. For example, as mentioned previously, an int can be implicitly converted to a double. An implicit conversion requires no special syntax and never throws an exception.

Click here to view code image

```
Example.MyDoubleMethod(42); // implicit int-to-double conversion
```

An implicit conversion is sometimes called a widening conversion because the result is wider than the original value—it contains at least as much information as the original value, and nothing is lost. In the case of int and double, the range of double is greater than that of int, and all int values have an equivalent double value. However, the converse is not true, and a double value cannot be implicitly converted to an int:

Click here to view code image

```
class Example
{
    public static void MyIntMethod(int parameter)
    {
        ...
    }
}
...
Example.MyIntMethod(42.0); // compile-time error
```

When you convert a double to an int, you run the risk of losing information, so the conversion will not be performed automatically. (Consider what would happen if the argument to MyIntMethod were 42.5. How should this be converted?) A double can be converted to an int, but the conversion requires an explicit notation (a cast):

Click here to view code image

```
Example.MyIntMethod((int)42.0);
```

An explicit conversion is sometimes called a narrowing conversion because the result is narrower than the original value (that is, it can contain less information) and can throw an OverflowException exception if the resulting value is out of the range of the target type. In C#, you can create conversion operators for your own user-defined types to control whether it is sensible to convert values to other types, and you can also specify whether these conversions are implicit or explicit.
