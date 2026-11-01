
```
uint bal = 350;
Currency balance = bal;
uint bal2 = (uint)balance;
```

The answer is not 350 but 3! Moreover, it all follows logically. You convert 350 implicitly to a Currency, giving the result balance.Dollars = 3, balance.Cents = 50. Then the compiler does its usual figuring out of the best path for the conversion back. Balance ends up being implicitly converted to a float (value 3.5), and this is converted explicitly to a uint with value 3.

Of course, other instances exist in which converting to another data type and back again causes data loss. For example, converting a float containing 5.8 to an int and back to a float again will lose the fractional part, giving you a result of 5, but there is a slight difference in principle between losing the fractional part of a number and dividing an integer by more than 100. Currency has suddenly become a rather dangerous class that does strange things to integers!

The problem is that there is a conflict between how your casts interpret integers. The casts between Currency and float interpret an integer value of 1 as corresponding to one dollar, but the latest uint-to-Currency cast interprets this value as one cent. This is an example of very poor design. If you want your classes to be easy to use, you should make sure that all your casts behave in a way that is mutually compatible, in the sense that they intuitively give the same results. In this case, the solution is obviously to rewrite the uint-to-Currency cast so that it interprets an integer value of 1 as one dollar:

```
public static implicit operator Currency (uint value)
{
    return new Currency(value, 0);
}
```

Incidentally, you might wonder whether this new cast is necessary at all. The answer is that it could be useful. Without this cast, the only way for the compiler to carry out a uint-to-Currency conversion would be via a float. Converting directly is a lot more efficient in this case, so having this extra cast provides performance benefits, though you need to make sure it gives the same result as via a float, which you have now done. In other situations, you may also find that separately defining casts for different predefined data types allows more conversions to be implicit rather than explicit, though that is not the case here.

A good test of whether your casts are compatible is to ask whether a conversion will give the same results (other than perhaps a loss of accuracy as in float-to-int conversions), regardless of which path it takes. The Currency class provides a good example of this. Look at this code:

```
Currency balance = new Currency(50, 35);
ulong bal = (ulong) balance;
```

At present, there is only one way that the compiler can achieve this conversion: by converting the Currency to a float implicitly, then to a ulong explicitly. The float-to-ulong conversion requires an explicit conversion, but that is fine because you have specified one here.

Suppose, however, that you then added another cast, to convert implicitly from a Currency to a uint. You will actually do this by modifying the Currency struct by adding the casts both to and from uint. This code is available as the SimpleCurrency2 example:

```
public static implicit operator Currency (uint value)
{
    return new Currency(value, 0);
}

public static implicit operator uint (Currency value)
{
    return value.Dollars;
}
```

Now the compiler has another possible route to convert from Currency to ulong: to convert from Currency to uint implicitly, then to ulong implicitly. Which of these two routes will it take? C# has some precise rules about the best route for the compiler if there are several possibilities. (The rules are not detailed in this book, but if you are interested, details are in the MSDN documentation.) The best answer is that you should design your casts so that all routes give the same answer (other than possible loss of precision), in which case it doesn't really matter which one the compiler picks. (As it happens in this case, the compiler picks the Currency-to-uint-to-ulong route in preference to Currency-to-float-to-ulong.)

To test the SimpleCurrency2 sample, add this code to the test code for SimpleCurrency:

```
try
{
    Currency balance = new Currency(50,35);
    Console.WriteLine(balance);
    Console.WriteLine("balance is " + balance);
    Console.WriteLine("balance is (using ToString()) " + balance.ToString());
    uint balance3 = (uint) balance;
    Console.WriteLine("Converting to uint gives " + balance3);
}
```

code snippet SimpleCurrency2/Program.cs

Running the sample now gives you these results:

## SIMPLECURRENCY2

```
50
balance is $50.35
balance is (using ToString()) $50.35
Converting to uint gives 50
After converting to float, = 50.35
After converting back to Currency, = $50.34
Now attempt to convert out of range value of -$50.50 to a Currency:
Result is $4294967246.00
```

The output shows that the conversion to uint has been successful, though as you have lost the cents part of the Currency in making this conversion. Casting a negative float to Currency has also produced the expected overflow exception now that the float-to-Currency cast itself defines a checked context.

However, the output also demonstrates one last potential problem that you need to be aware of when working with casts. The very first line of output has not displayed the balance correctly, displaying 50 instead of $50.35. Consider these lines:

```
Console.WriteLine(balance);
Console.WriteLine("balance is " + balance);
Console.WriteLine("balance is (using ToString()) " + balance.ToString());
```

Only the last two lines correctly display the Currency as a string. So what is going on? The problem here is that when you combine casts with method overloads, you get another source of unpredictability. We will look at these lines in reverse order.

The third Console.WriteLine() statement explicitly calls the Currency.ToString() method, ensuring that the Currency is displayed as a string. The second does not do so. However, the string literal "balance is" passed to Console.WriteLine() makes it clear to the compiler that the parameter is to be interpreted as a string. Hence, the Currency.ToString() method will be called implicitly.

The very first Console.WriteLine() method, however, simply passes a raw Currency struct to Console.WriteLine(). Now, Console.WriteLine() has many overloads, but none of them takes a Currency struct. So the compiler will start fishing around to see what it can cast the Currency to in order to make it match up with one of the overloads of Console.WriteLine(). As it happens, one of the Console.WriteLine() overloads is designed to display uints quickly and efficiently, and it takes a uint as a parameter — you have now supplied a cast that converts Currency implicitly to uint.

You call up these methods like this:

```csharp
using System;

namespace Wrox.ProCSharp.Delegates
{
    delegate double DoubleOp(double x);

    class Program
    {
        static void Main()
        {
            DoubleOp[] operations =
            {
                MathOperations.MultiplyByTwo,
                MathOperations.Square
            };

            for (int i=0; i < operations.Length; i++)
            {
                Console.WriteLine("Using operations[{0}]: ", i);
                ProcessAndDisplayNumber(operations[i], 2.0);
                ProcessAndDisplayNumber(operations[i], 7.94);
                ProcessAndDisplayNumber(operations[i], 1.414);
                Console.WriteLine();
            }

            static void ProcessAndDisplayNumber(DoubleOp action, double value)
            {
                double result = action(value);
                Console.WriteLine(
                    "Value is {0}, result of operation is {1}", value, result);
            }
        }
    }
}
```

code snippet SimpleDelegate/Program.cs

In this code, you instantiate an array of DoubleOp delegates (remember that after you have defined a delegate class, you can basically instantiate instances just as you can with normal classes, so putting some into an array is no problem). Each element of the array gets initialized to refer to a different operation implemented by the MathOperations class. Then, you loop through the array, applying each operation to three different values. This illustrates one way of using delegates — that you can group methods together into an array using them, so that you can call several different methods in a loop.

The key lines in this code are the ones in which you actually pass each delegate to the ProcessAndDisplayNumber() method, for example:

```
ProcessAndDisplayNumber(operations[i], 2.0);
```

Here, you are passing in the name of a delegate but without any parameters. Given that operations[i] is a delegate, syntactically:

- operations[i] means the delegate (that is, the method represented by the delegate).
- operations[i] (2.0) means actually call this method, passing in the value in parentheses.
