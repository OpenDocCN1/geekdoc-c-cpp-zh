# CHAPTER 7 Using Methods

# TWO TRUTHS & A LIE

# Writing Methods That Require Multiple Arguments

+   1. The following is a usable C# method header:
   private static void MyMethod(double amt, sum)
2. The following is a usable C# method header:
   private static void MyMethod2(int x, double y)
3. The following is a usable C# method header:
   static void MyMethod3(int id, string name, double rate)

> does not contain an accessibility indicator, but is optional.
type, even if the header in #3 are the same. The parameters for all data types
The false statement is #1. In a method header, each parameter must have a data

# Writing Methods That Return Value

A method can return, at most, one value to the method that it calls. The return type for a method can be any type used in the C# programming language, which includes the basic built-in types int, double, and so on. You can also use a class as the return type for method, including any type built into the C# language. For example, you have used a returned value from the ReadLine() method when writing a statement as inputString = ReadLine(); Because the ReadLine() method can be assigned to a string, its return type is string. In Chapter 3 you learned about control types, such as Button and Label. Objects of these types you learn to create your own types in Chapter 9, and these can be returned from a method too. Of course, a method also can return nothing, in which case the return value is void.

For example, suppose that you want to create a method to accept the hours an employee worked and the hourly pay rate, and to return a calculated gross pay value. The header for this method could be:

private static double CalPay(double hours, double rate)

Figure 7-13 shows this method.

```
private static double CalPay(double hours, double rate)
{
    double gross;
    gross = hours * rate;
    return gross;
}
```

Figure 7-13 The CalPay() method