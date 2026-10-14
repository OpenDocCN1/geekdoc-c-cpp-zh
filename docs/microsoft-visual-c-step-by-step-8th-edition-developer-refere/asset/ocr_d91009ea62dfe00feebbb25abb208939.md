```
temp = first / second;
Console.WriteLine($"Divide: result is {temp}");
}
```

This code creates two Complex objects that represent the complex values (10 + 4i) and (5 + 2i). The code displays them and then tests each of the operators you have just defined, displaying the results in each case.

11. On the Debug menu, click Start Without Debugging.

Verify that the application displays the results shown in the following image:

![](bbox=[0.26, 0.26, 0.72, 0.4])

12. Close the application, and return to the Visual Studio 2015 programming environment.

You have now created a type that models complex numbers and supports basic arithmetic operations. In the next exercise, you will extend the Complex class and provide the equality operators, == and !=.

# Implement the equality operators

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