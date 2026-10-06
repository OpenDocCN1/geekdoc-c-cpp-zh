
# You Do It

# Calling a Method

In this section, you write a program in which a Main() method calls another method that displays a company's logo.

- 1. Open a new program named DemoLogo, and enter the statement that allows the program to use System.Console methods without qualifying them. Then type the class header for the DemoLogo class and the class-opening brace.

```csharp
using static System.Console;
class DemoLogo
{}
```

- 2. Type the Main() method for the DemoLogo class. This method displays a line, then calls the DisplayCompanyLogo() method.

```csharp
static void Main()
{
   Write("Our company is ");
   DisplayCompanyLogo();
}
```

- 3. Add a method that displays a two-line logo for a company.
```csharp
private static void DisplayCompanyLogo()
{
   WriteLine("See Sharp Optical");
   WriteLine("We prize your eyes");
}
```

- 4. Add the closing curly brace for the class { } }, and then save the file.

- 5. Compile and execute the program. The output should look like Figure 7-7.

```
Our company is See Sharp Optical
We prize your eyes
```

Figure 7-7 Output of the DemoLogo program

(continues)

# CHAPTER 7 Using Methods

(continued)

- 6. Remove the keyword static from the DisplayCompanyLogo() method, and then save and compile the program. An error message appears, as shown in Figure 7-8. The message indicates that an object reference is required for the nonstatic DisplayCompanyLogo() method. The error occurs because the Main() method is static and cannot call a nonstatic method without an object reference (that is, without using an object name and a dot before the method call). Remember that you will learn to create objects in Chapter 9, and that you can create types of methods that do not use the keyword static. For now, retype the keyword static in the DisplayCompanyLogo() method header, and compile and execute the program again.

```
DemoLogo.cs(7,2): error CS0120: An object reference is required for the non-static field, or property 'DemoLogo.DisplayCompanyLogo()'
```

**Figure 7-8** Error message when calling a nonstatic method from a static method

- 7. Remove the keyword private from the header of the DisplayCompanyLogo() method. Save and compile the program, and then execute it. The execution is successful because the private keyword is optional. Replace the private keyword, and save the program.

# Writing Methods That Require a Single Argument

Some methods require additional information. If a method could not receive arguments, then you would have to receive an infinite number of methods to cover every possible situation. For example, when you make a dental appointment, you do not need to employ a different method for every date of the year at every possible time of day. Rather, you can supply the date and time as information to the method, and no matter what date and time you supply, the method is carried out correctly. If you design a method to compute an employee's paycheck, you could write a method named ComputePaycheck() and supply it with an hourly rate rather than developing methods with names like ComputePaycheckAtFourteenDollarsPerHour(), ComputePaycheckAtFifteenDollarsPerHour(), and so on.

You have already used methods to supply a wide variety of parameters. By any call, the Line() method can receive any one of an infinite number of strings as a parameter—"Hello", "Goodbye", and so on. No matter what message you send to the Line() method, the message is displayed correctly.

# Writing Methods That Require a Single Argument

When you write the declaration for a method that accepts a parameter, you need to include the following items within the method declaration parentheses:

- The data type of the parameter
- A local identifier (name) for the parameter.

For example, consider a method named DisplaySalesTax(), which computes and displays a tax as 7 percent of a selling price. The method header for a usable DisplaySalesTax() could be the following:

```csharp
static void DisplaySalesTax(double saleAmount)
```

You can think of the parentheses in a method declaration as a funnel into the method—parameters listed there are "dropping in" to the method.

The parameter double saleAmount within indicates that the DisplaySalesTax() method will receive a value of type double. Within the method, the value will be known as saleAmount. Figure 7-9 shows a complete method.

```csharp
private static void DisplaySalesTax(double saleAmount)
{
    const double RATE = 0.07;
    double tax = saleAmount * RATE;
    WriteLine("The tax on {0} is {1}",
        saleAmount, tax.ToString("C"));
}
```

Figure 7-9 The DisplaySalesTax() method

![](img/7516c1fecf7bbbe7afb10cf209b17ae3_303_0.png)

> Within the DisplaySalesTax() method, you must use the format string and ToString() method if you want figures to display exactly two decimal positions. You learned how to display values to a fixed number of decimal places in Chapter 2; recall that using the fixed format with no number defaults to two decimal places.

You create the DisplaySalesTax() method as a void method (one that has a void return type) because you do not need it to return to any method that uses it—only its function is to receive the saleAmount value, multiply it by 0.07, and then display the result. You create it as a static method because you do not want the Main() method to be required to create an object with which to use it; you want the static Main() method to be able to call the method directly.

# CHAPTER 7 Using Methods

Within a program, you can call the DisplaySalesTax() method using the method's name and, in parentheses, an argument that is either a constant value or a variable. Thus, assuming myPurchase is a declared double variable with an assigned value, both of the following calls to the DisplaySalesTax() method invoke it correctly:

```csharp
DisplaySalesTax(12.99);
DisplaySalesTax(myPurchase);
```

You can call the DisplaySalesTax() method any number of times, with a different constant or argument value each time. The value of each of these becomes known as saleAmount within the method. Interestingly, if the argument in the method call is a variable, it might possess the same identifier as saleAmount or one other, as myPurchase. The identifier saleAmount is simply the name “goes by” while being used within the method, no matter what name it uses in the calling program. That is, variable saleAmount is a local variable to the DisplaySalesTax() method, as variables and constants declared within.

The variable saleAmount declared in the method header is a formal parameter. In contrast, arguments within a call are referred to as actual parameters. For example, in the calling statement DisplaySalesTax(myPurchase); myPurchase is an actual parameter.

> The formal parameter saleAmount also is an example of value parameter. You will learn more about value parameters in the next chapter.

The DisplaySalesTax() method employs hiding. That is, if a programmer changes the way the tax is calculated—for example, by coding one—programs that use the DisplaySalesTax() method will not be affected and will not need to be modified:

```csharp
tax = saleAmount * 7 / 100;
tax = 0.07 * saleAmount;
```

No matter how the tax is calculated, a calling program passes a value into the DisplaySalesTax() method, and a calculated result appears on the screen.

Figure 7-10 shows a complete program called UseMethod. It uses the DisplaySalesTax() method twice, first with a argument, and then with a constant argument. The program’s output appears in Figure 7-11.

![](img/7516c1fecf7bbbe7afb10cf209b17ae3_304_0.png)

```csharp
using static System.Console;
class UseMethod
{
    static void Main()
    {
        double myPurchase = 12.99;
        DisplaySalesTax(myPurchase);
        DisplaySalesTax(35.67);
    }
    private static void DisplaySalesTax(double saleAmount)
    {
        double tax;
        const double RATE = 0.07;
        tax = saleAmount * RATE;
        WriteLine("The tax on {0} is {1}", saleAmount, tax.ToString("C"));
    }
}
```

**Figure 7-10** Complete program using the DisplaySalesTax() method two times

![](img/7516c1fecf7bbbe7afb10cf209b17ae3_305_0.png)

**Figure 7-11** Output of the UseMethod program

An argument type in a method can match the method's parameter type exactly, but it can use a different data type if the argument can be converted automatically to the parameter type. Recall from Chapter 2 that C# supports the following automatic conversions:

- From byte to short, int, long, float, double, or decimal
- From byte to short, ushort, int, uint, long, float, double, or decimal
- From short to int, long, float, double, or decimal
- From ushort to int, uint, long, float, double, or decimal
- From int to long, float, double, or decimal
- From uint to long, long, float, double, or decimal
- From long to float, double, or decimal
- From ulong to float, double, or decimal
- From char to ushort, int, uint, long, float, double, or decimal
- From float to double
