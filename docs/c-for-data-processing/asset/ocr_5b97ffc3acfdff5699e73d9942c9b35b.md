```
```csharp
using System;

class GlazerCalc
{
    static void Main()
    {
        double width, height, woodlength, glassArea;
        const double MAX_WIDTH = 5.0;
        const double MIN_WIDTH = 0.5;
        const double MAX_HEIGHT = 3.0;
        const double MIN_HEIGHT = 0.75;
        string widthString, heightString;

        do {
            Console.Write ( "Give the width of the window between " + 
            MIN_WIDTH + " and " + MAX_WIDTH + ": " );
            widthString = Console.ReadLine();
            width = double.Parse(widthString);
        } while ( width < MIN_WIDTH || width > MAX_WIDTH );

        do {
            Console.Write ( "Give the height of the window between " + 
            MIN_HEIGHT + " and " + MAX_HEIGHT + ": " );
            heightString = Console.ReadLine();
            height = double.Parse(heightString);
        } while ( height < MIN_HEIGHT || height > MAX_HEIGHT );

        woodlength = 2 * ( width + height ) * 3.25 ;
        glassArea = 2 * ( width * height ) ;

        Console.WriteLine ( "The length of the wood is " + 
        woodlength + " feet" ) ;
        Console.WriteLine( "The area of the glass is " + 
        glassArea + " square metres" ) ;
    }
}
```
```

# 2.3.4 Operator Shorthand

So far we have looked at operators which appear in expressions and work on two operands, e.g.

```
window_count = window_count + 1
```

In this case the operator is + and is operating on the variable window_count and the value 1. The purpose of the above statement is to add 1 to the variable window_count. However, it is a rather long winded way of expressing this, both in terms of what we have to type and what the computer will actually do when it runs the program. C# allows us to be terser if we wish, the line:

```
window_count++
```

would do the same thing. We can express ourselves more succinctly and the compiler can generate more efficient code because it now knows that what we are doing is adding one to a particular variable. The ++ is called a unary operator, because it works on just one operand. It causes the value in that operand to be increased by one. There is a corresponding -- operator which can be used to decrease (decrement) variables. You can see examples of this construction in the for loop definition in the example above.