# 244 Returning Values after Christmas

```
// This also works.
Console.WriteLine("The average of * + v1 \
      + * + v2 + is \
      + Average(v1
```

Notice first that I declare the method public static double Average() — the double in front of its name indicates that the Average method returns a double-precision value to the caller.

The Average method passes the names d1 and d2 to the values passed to it. This method creates a variable average to which it assigns the average of d1 and d2 returns to the caller the value contained in average.

People sometimes use this careless common shorthand: "The method returns average." Saying that average or any other value is passed or returned anywhere. In this case, the value contained within average is returned to the caller.

![](bbox=[0.137, 0.376, 0.218, 0.435])

The call to Average() from the Test() returns the same as any other method; however, the double value returned by Average() via the return is stored in the averageValue.

A method that returns a value, as Average(), cannot return to the caller by merely encountering the close brace of the method. If it did, C# wouldn't know which value to return. You need a return statement.

![](bbox=[0.137, 0.523, 0.218, 0.582])

# Defining a method with no value

The declaration public static double Average(double, double) declares a method Average() that returns the average of its arguments as a double. (The number returned had better be the average of the input values or else has some serious explaining to)

Some methods not need to return a value to the caller. The earlier method AverageAndDisplay() example displays the average of its arguments but does not return the value to the caller. (That idea may be a good one, but is not to question.) Rather than leave the type blank, you declare a method such as AverageAndDisplay() this way:

```
void AverageAndDisplay(double, double)
```

The keyword void, where the return type is normally used, means nontype. That is, the declaration void indicates that the AverageAndDisplay() method returns no value to the caller. (Regardless, every declaration specifies a return type, even if it's void.)